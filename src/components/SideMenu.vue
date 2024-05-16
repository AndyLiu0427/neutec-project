<template>
  <div class="sidebar" v-if="data && data.length">
    <ul class="list-items">
      <SideMenuItem
        v-for="item in data"
        :key="item.key"
        :item="item"
        @update-active="updateActive"
        @toggle-menu="toggleMenu"
      />
    </ul>
  </div>
</template>

<script setup>
import SideMenuItem from './SideMenuItem.vue';
import { onMounted, ref } from 'vue';

const data = ref([]);

const fetchData = async () => {
  try {
    const response = await fetch('./data.json')
    if (response.ok) {
      data.value = await response.json()
      console.log('Data fetched:', data.value)
    } else {
      console.error('Failed to fetch data')
    }
  } catch (error) {
    console.error('Error fetching data:', error)
  }
}

onMounted(() => {
  fetchData()
})

const updateActive = (activeItem) => {
  if (data.value) {
    data.value.forEach(item => {
      if (item !== activeItem) {
        item.active = false;
      }
    });
    activeItem.active = true;
  }
}

const toggleMenu = (activeItem) => {
  if (data.value) {
    data.value.forEach(item => {
      if (item !== activeItem && item.children) {
        item.expanded = false;
      }
    });
  }
}
</script>

<style>
  .active {
    background: #808080;
  }
  .active > span {
    color: yellow;
  }
</style>
