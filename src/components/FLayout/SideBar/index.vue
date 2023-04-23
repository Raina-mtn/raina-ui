<template>
  <el-scrollbar wrap-class="scrollbar-wrapper">
    <el-menu
      class="el-menu-vertical"
      mode="vertical"
      :collapse="!opened"
      :background-color="menuBg"
      :text-color="menuTextColor"
      :active-text-color="menuActiveTextColor"
      :collapse-transition="false"
      :default-active="activeMenu"
    >
      <SidebarItem v-for="item in menu" :key="item.path" :route="item" />
    </el-menu>
  </el-scrollbar>
</template>

<script>
import SidebarItem from '../SideBar/SidebarItem.vue';
export default {
  name: "Sidebar",
  components: {
    SidebarItem
  },
  props: {
    opened: {
      type: Boolean
    },
    menu: {
      type: Array,
      default: () => []
    },
    // 菜单背景颜色，（仅支持 hex 格式，即'#fff'）
    menuBg: {
      type: String,
      default: ''
    },
    // 菜单文字颜色，（仅支持 hex 格式，即'#fff'）
    menuTextColor: {
      type: String,
      default: ''
    },
    // 菜单激活文字颜色，（仅支持 hex 格式，即'#fff'）
    menuActiveTextColor: {
      type: String,
      default: ''
    }
  },
  computed: {
    activeMenu() {
      const route = this.$route
      const { meta, path } = route
      if (meta.activeMenu) {
        return meta.activeMenu
      }

      return path
    }
  }

}
</script>

<style>
</style>
<style lang="scss">
.el-scrollbar__view {
  height: 100%;
}
</style>