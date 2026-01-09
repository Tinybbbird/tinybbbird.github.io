---
title: 机场节点套 WARP 解决 Google 送中及 Gemini 不可用问题
date: 2026-01-09
tags:
  - Clash
  - WARP
  - 网络优化
---

## 问题背景
虽然开启了美国节点，但 **Gemini** 网页显示“当前地区不支持”，且 Google 搜索结果显示在中国区。这是因为机场节点 IP 使用人数过多，被 Google 识别并“送中”。

**解决方案：** 通过 Clash 链式代理，在现有节点基础上套一层 **Cloudflare WARP**，隐藏原始节点 IP。

## 一、 获取 WARP 注册配置

### 1. 下载工具
从 GitHub 下载 [wgcf](https://github.com/ViRb3/wgcf) 对应系统的版本。
> **wgcf**: 一个强大的命令行工具，用于将 Cloudflare WARP 服务转换为通用的 WireGuard 配置文件。

### 2. 生成配置
在终端（CMD 或 PowerShell）中进入工具所在目录，依次执行以下命令：

```bash
wgcf.exe register  # 注册账号
wgcf.exe generate  # 生成配置文件
```
执行后生成2个文件：  
` wgcf-account.toml `：账户信息  
` wgcf-profile.conf `：WireGuard 连接参数 
 
### 3. **获取配置参数**
**打开 `wgcf-profile.conf`，记录以下信息备用：**
`PrivateKey`
`Address`（IPv4 和 IPv6 地址）
`PublicKey`（固定值：bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=）
`Endpoint`（engage.cloudflareclient.com:2408）

# 二、clash配置
**在新版Clash Verge 的全局扩展脚本中输入：**
```javascript
function main(config, profileName) {
  let proxies = [
    {
      name: "美国-WARP",
      type: "wireguard",
      server: "162.159.192.20",
      port: 2408,
      ip: "你的IPv4地址", // 填入 Address 中的 IPv4
      ipv6: "你的IPv6地址", // 填入 Address 中的 IPv6
      "private-key": "你的PrivateKey", // 填入上文提取的 PrivateKey
      "public-key": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
      udp: true,
      mtu: 1280,
      "dialer-proxy": "WARP前置-美国",
      "dial-timeout": 60000,
    },
  ];//自定义代理
  let proxyGroup = [
    {
      name: "WARP前置-美国",
      type: "fallback",
      "include-all": true,
      filter:
        "(?i)^(?!.*WARP).*(美|波特兰|达拉斯|俄勒冈|凤凰城|费利蒙|硅谷|拉斯维加斯|洛杉矶|圣何塞|圣克拉拉|西雅图|芝加哥|US|United States)",
      url: "https://www.gstatic.com/generate_204",
      interval: 60,
      timeout: 5000,
    },
    {
      name: "Gemini",
      type: "select",
      proxies: ["美国-WARP"],
    },
  ];//自定义代理组
  let rules = ["GEOSITE,google-deepmind,Gemini"]; //自定义分流规则：geosite是社区维护通用规则
  config.proxies = proxies.concat(config.proxies);
  config["proxy-groups"] = proxyGroup.concat(config["proxy-groups"]);
  config.rules = [...config.rules,...rules];
  return config;
}

```
**说明**
- `ip4`和`ip6`填`address`中对应地址
- `private-key`填写`PrivateKey`
- `dialer-proxy` 指定前置节点组，流量会先经过机场美国节点，再通过 WARP 隧道。