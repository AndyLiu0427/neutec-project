<template>
  <li :class="`${ item.active ? 'active' : '' }`" @click="toggleMenu">
    <span>{{ item.text }}</span>
    <ul v-show="item.children && item.expanded">
      <side-menu-item
        v-for="child in item.children"
        :item="child"
        :key="child.key"
        :class="`${ item.children.active ? 'active' : '' }`"
        @update-active="handleUpdateActive"
        @toggle-menu="handleToggleMenu"
      />
    </ul>
  </li>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true
    }
  },
  methods: {
    toggleMenu() {
      if (this.item.children) {
        this.item.expanded = !this.item.expanded;
        if (!this.item.expanded) {
          this.item.active = false;
        }
      }
      this.$emit('update-active', this.item);
      this.$emit('toggle-menu', this.item);
    },
    handleUpdateActive(clickedItem) {
      this.item.active = (this.item === clickedItem) ? true : false;
      if (this.item.children) {
        this.item.children.forEach(child => {
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
      this.$emit('update-active', this.item);
    },
    handleToggleMenu(clickedItem) {
      if (this.item === clickedItem) {
        this.item.expanded = !this.item.expanded;
      } else {
        this.item.expanded = false;
      }
      this.item.children.forEach(child => {
        if (child !== clickedItem) {
          child.expanded = false;
        } else {
          child.expanded = true;
        }
      });
    }
  }
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
