<script setup lang="ts">
import { RouterView } from 'vue-router'
import HeaderComponent from './components/HeaderComponent.vue'
import FooterComponent from './components/FooterComponent.vue';
</script>

<template>
  
  <HeaderComponent></HeaderComponent>

  <RouterView />

  <FooterComponent></FooterComponent>

</template>

<style scoped>

</style>
