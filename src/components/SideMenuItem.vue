<template>
  <li :class="`${item.active ? 'active' : ''}`" @click="toggleMenu">
    <span>{{ item.text }}</span>
    <ul v-show="item.children && item.expanded">
      <SideMenuItem
        v-for="child in item.children"
        :key="child.key"
        :item="child"
        @update-active="handleUpdateActive"
        @toggle-menu="handleToggleMenu"
      />
    </ul>
  </li>
</template>

<script setup>
import { ref, defineProps } from 'vue';
const emit = defineEmits(['update-active', 'toggle-menu', 'update-active'])
const props = defineProps({
  item: {
    type: Object,
    required: true
  }
});


const toggleMenu = () => {
  if (props.item.children) {
    props.item.expanded = !props.item.expanded;
    if (!props.item.expanded) {
      props.item.active = false;
    }
  }
  emit('update-active', props.item);
  emit('toggle-menu', props.item);
};

const handleUpdateActive = (clickedItem) => {
  props.item.active = props.item === clickedItem;
  if (props.item.children) {
    props.item.children.forEach(child => {
      if (child !== clickedItem) {
        child.active = false;
        if (child.children) {
          child.children.forEach(c => {
            c.active = false;
          });
        }
      } else {
        child.active = true;
      }
    });
  }
  emit('update-active', props.item);
};

const handleToggleMenu = (clickedItem) => {
  if (props.item === clickedItem) {
    props.item.expanded = !props.item.expanded;
  } else {
    props.item.expanded = false;
  }
  props.item.children.forEach(child => {
    if (child !== clickedItem) {
      child.expanded = false;
    } else {
      child.expanded = true;
    }
  });
};
</script>

<style>
.active {
  background: #808080;
}

.active > span {
  color: yellow;
}
</style>
