<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import StartPage from './components/startPage.vue'
import { searchList } from './db'
</script>

<template>
  <StartPage :data="searchList" />
</template>

<style scoped>
@import url('./assets/css/style.css');
</style>
