<template>
  <nav>
    <button class="menu-button" @click="toggleSideMenu">&#9776;</button>
    <side-menu
      :class="{ showMenu: showSideMenu, hideMenu: !showSideMenu}"
      :data="menuData"
      ref="sideMenuRef"
    />
  </nav>
  <div class="main">
    <Game />
  </div>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue'
import SideMenu from './SideMenu.vue'
import Game from './Game.vue'

const showSideMenu = ref(false)
const sideMenuRef = ref(null);

function toggleSideMenu() {
  showSideMenu.value = true;
  console.log('toggleSideMenu', showSideMenu.value);
}

const handleClickOutside = (event) => {
  if (showSideMenu.value === false) return;

  const listItems = document.querySelectorAll('.list-items');
  const menuButton = document.querySelector('.menu-button');

  if (event.target === menuButton) return;

  console.log('listItems:', listItems);
  let isClickOutside = true;
  listItems.forEach(item => {
    console.log('item:', item);
    if (item.contains(event.target)) {
      isClickOutside = false;
    }
  });
  if (isClickOutside) {
    console.log('Click outside');
    showSideMenu.value = false; // 隱藏側邊選單
  }
}

const menuData = ref([])

async function fetchData() {
  try {
    const response = await fetch('/data.json')
    if (response.ok) {
      menuData.value = await response.json()
      console.log('Data fetched:', menuData.value)
    } else {
      console.error('Failed to fetch data')
    }
  } catch (error) {
    console.error('Error fetching data:', error)
  }
}

onMounted(() => {
  fetchData()
  document.addEventListener('click', handleClickOutside);
})

onUnmounted(() => {
  document.removeEventListener('click', handleClickOutside);
});

</script>

<style lang="css">
@import '../assets/css/style.css';
</style>
