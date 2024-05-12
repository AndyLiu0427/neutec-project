<template>
  <div class="sidebar">
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

<script>
import SideMenuItem from './SideMenuItem.vue';

export default {
  props: {
    data: {
      type: Array,
      required: true
    }
  },
  components: {
    SideMenuItem
  },
  methods: {
    updateActive(activeItem) {
      this.data.forEach(item => {
        if (item !== activeItem) {
          item.active = false;
        }
      });
      activeItem.active = true;
    },
    toggleMenu(activeItem) {
      this.data.forEach(item => {
        if (item !== activeItem && item.children) {
          item.expanded = false;
        }
      });
    }
  }
};
</script>
