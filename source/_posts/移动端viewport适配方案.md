---
title: 移动端viewport适配方案
date: 2021-12-27 14:01:55
categories:
- 技术
tags:
- 前端
- css
---
## vw和vh介绍
vw（Viewport Width）、vh(Viewport Height)是基于视图窗口的单位，除了vw、vh还有vmin、vmax。

vw:1vw等于视口宽度的1%
vh:1vh等于视口宽度的1%
vmin:vw和vh中小的那个
vmax:vw和vh中大的那个

假设拿到750px的设计图，那么1vw=750/100=7.5px,图上宽度是75px的元素转化过来就是10vw

## 结合sass转换px单位
{% codeblock lang:css %}
$base_width: 750;
$base_height: 1080;
@function vw($px) {
  @return ($px / $base_width) * 100vw;
}
@function vh($px) {
  @return ($px / $base_height) * 100vh;
}
{% endcodeblock %}

