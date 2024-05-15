<template>
  <div class="container">
    <div class="grid-container">
      <div class="grid-item" v-for="i in 9" :key="i"></div>
    </div>
    <div class="ball-container">
      <div
        v-for="cell in cells"
        :key="cell.id"
        :style="`${cell.show ? 'opacity: 1' : 'opacity: 0'};`"
        class="ball-block"
      >
        <div>
          <div class="ball">0</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const cells = ref([
  { id: 1, show: true },
  { id: 2, show: false },
  { id: 3, show: true },
  { id: 4, show: false },
  { id: 5, show: false },
  { id: 6, show: false },
  { id: 7, show: true },
  { id: 8, show: false },
  { id: 9, show: true }
]);
</script>
