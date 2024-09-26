<template>
  <p class="text-center text-[#666]">
    Copyright © 新疆萌森软件开发工作室 {{ year }}
    <a href="https://blog.lifebus.top/" target="_blank">人生足迹 · 博客平台</a>
  </p>
</template>
<script lang="ts" setup>
import { ref } from 'vue';
const year = ref(new Date().getFullYear());
</script>
