<template>
  <div class="sidebar">
    <ul class="list-items">
      <li v-for="item in data" :key="item.key">
        {{ item.text }}
        <!-- <ul v-if="item.children">
          <li v-for="child in item.children" :key="child.key">
            {{ child.text }}
          </li>
        </ul> -->
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  data: {
    type: Array,
    required: true
  }
})
</script>

<style scoped>
.side-menu {
  width: 200px;
}
</style>