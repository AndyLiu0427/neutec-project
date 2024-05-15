<template>
  <nav>
    <button class="menu-button" @click="toggleSideMenu">&#9776;</button>
    <SideMenu :class="{ showMenu: showSideMenu, hideMenu: !showSideMenu}" />
  </nav>
  <div class="main">
    <Game />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import SideMenu from './SideMenu.vue'
import Game from './Game.vue'

const showSideMenu = ref(false);

const toggleSideMenu = () => {
  showSideMenu.value = true;
}

const handleClickOutside = (event) => {
  if (!showSideMenu.value) return;

  const sidebar = document.querySelector('.sidebar');
  const menuButton = document.querySelector('.menu-button');

  const isClickInsideMenu = sidebar.contains(event.target) || menuButton.contains(event.target);

  if (!isClickInsideMenu) {
    showSideMenu.value = false;
  }
}

onMounted(() => {
  document.addEventListener('click', handleClickOutside);
})

onUnmounted(() => {
  document.removeEventListener('click', handleClickOutside);
});
</script>

<style lang="css">
@import '../assets/css/style.css';
</style>
