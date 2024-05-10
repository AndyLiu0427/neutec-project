<template>
  <router-view />
</template>

<script setup>
import Home from './components/Home.vue'

const routes = [
  { path: '/', component: Home }
]

</script>