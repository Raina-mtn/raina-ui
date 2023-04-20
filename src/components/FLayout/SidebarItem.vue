<template>
  <div v-if="!route.hidden">
    <!-- 
      1.父菜单无子菜单
      2.有且只有1个子菜单&&子菜单无children&&不要求显示父菜单保持嵌套形式
    -->
    <template v-if="hasOneShowingChild(route.children,route) && (!onlyOneChild.children || onlyOneChild.noShowingChildren) && !route.alwaysShow">
      <router-link :to="onlyOneChild.path">
        <el-menu-item>
          <Item
            :icon="onlyOneChild.meta.icon"
            :title="routeTitle(route.mata.title)"
          />
        </el-menu-item>
      </router-link>
    </template>

    <el-submenu
      v-else
      :index="route.path"
    >
      <template slot="title">
        <Item
          v-if="route.meta && route.meta.title"
          :icon="route.meta.icon"
          :title="routeTitle(route.meta.title)"
        />
      </template>
      <!-- 递归调用组件本身 -->
      <SiderbarItem
        v-for="item in route.children"
        :key="item.path"
        :route="item"
      />
    </el-submenu>
  </div>
</template>

<script>
import Item from './Item.vue'
export default {
  name:'SiderbarItem',
  components: {
    Item
  },
  props:{
    //route
    route: {
      type: Object,
      default: () => {}
    }
  },
  data() {
    return {
      onlyOneChild:null,
    }
  },
  methods:{
    /**
     * @description: 用于判断是否只有一个子菜单，若只有一个则默认直接显示该子菜单不显示父菜单
     * @param {*} children 子菜单
     * @param {*} parent 当前菜单
     * @return {*}
     */
    hasOneShowingChild(children = [], parent){
      const showingChildren = children.filter(item=>{
        if(item.hidden)
          return false
        else{
          this.onlyOneChild = item
          return true
        }
      })
      //若只有一个子菜单，则直接显示该子菜单
      if (showingChildren.length === 1) {
        return true
      }

      //若无子菜单，则直接显示该菜单
      if(showingChildren.length === 0){
        this.onlyOneChild = { ... parent, noShowingChildren: true }
        return true
      }

      return false
    },
    /**
     * @description：判断是否需要使用i18n切换语言
     * @param {*} langkey 标题
     */
    routeTitle(langkey) {
      const name = `sidebar.${langkey}`
      if (this.$te && this.$te(name)) {
        return this.$t(name)
      }
      return langkey
    }
  }
}
</script>

<style>

</style>