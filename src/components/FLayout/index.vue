<template>
  <div>
    <el-menu
      mode="vertical"
      :collapse="!opened"
      :background-color="menuBg"
      :text-color="menuTextColor"
      :active-text-color="menuActiveTextColor"
      :collapse-transition="false"
    >
    <SidebarItem v-for="item in menu" :key="item.path" :route="item"></SidebarItem>
  </el-menu>
  </div>
</template>

<script>
import SidebarItem from './SidebarItem.vue';
export default {
  components:{
    SidebarItem
  },
  props:{
    opened: {
      type: Boolean
    },
    menu:{
      type:Array,
      default:()=>[]
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
    },
  }

}
</script>

<style>
</style>