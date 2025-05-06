---
title: js 判断是移动端浏览器还是 PC 端浏览器
date: 2021-12-17 13:23:16
categories:
- 技术
tags:
- 前端
- js

---
{% codeblock lang:js %}
if( /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent) ) {
    document.write("移动")
} else {
    document.write("PC")
}
{% endcodeblock %}