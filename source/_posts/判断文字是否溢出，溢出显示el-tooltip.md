---
title: 判断文字是否溢出，溢出显示el-tooltip
date: 2025-03-11 10:48:35
categories:
- 技术
tags:
- 前端
- vue
---

## 需要实现的功能
当前文本如果宽度超出规定的宽度，鼠标移上去用el-tooltip显示完整的文字，不超出则不显示。

{% codeblock lang:js %}
<template>
<div class="label">
  <el-tooltip placement="top" :disabled="!isShowTooltip" :content="item.title">
    <span @mouseenter="isTextOverflow($event)">文本内容</span>
  </el-tooltip>
</div>
</template>
<script setup>
const isShowTooltip = ref(false);
// 检查文本是否溢出
const isTextOverflow = (event) => {
  if (event && event.target) {
    if(event.target.scrollWidth > event.target.clientWidth) {
      isShowTooltip.value=true
    }else {
      isShowTooltip.value=false
    }
  }
  return false
}
</script>
<style scoped lang="scss">
  .label {
    width:225px; /* 调整为合适的宽度 */
    span {
      width:100%;
      display: inline-block;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
  }
</style>
{% endcodeblock %}
