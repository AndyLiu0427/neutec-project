<template>
  <nav>
    <button class="menu-button" @click="toggleSideMenu">&#9776;</button>
    <SideMenu
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
  // console.log('toggleSideMenu', showSideMenu.value);
}

function isDescendant(parent, child) {
  let node = child.parentNode;
  while (node !== null) {
    if (node === parent) {
      return true;
    }
    node = node.parentNode;
  }
  return false;
}

const handleClickOutside = (event) => {
  if (!showSideMenu.value) return;

  const sidebar = document.querySelector('.sidebar');
  const menuButton = document.querySelector('.menu-button');

  // 检查点击事件的目标是否在菜单或菜单按钮内部
  const isClickInsideMenu = sidebar.contains(event.target) || menuButton.contains(event.target);

  // 如果点击事件的目标不在菜单或菜单按钮内部，则关闭侧边栏
  if (!isClickInsideMenu) {
    showSideMenu.value = false;
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
