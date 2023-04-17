<template>
  <div v-if="!route.hidden">
    <!-- 
      1.父菜单无子菜单
      2.有且只有1个子菜单&&子菜单无children&&不要求显示父菜单保持嵌套形式
    -->
    <template v-if="hasOneShowingChild(route.children,route) && (!onlyOneChild.children || onlyOneChild.noShowingChildren) && !route.alwaysShow">
      <router-link :to="onlyOneChild.path">
        <el-menu-item>

        </el-menu-item>
      </router-link>
    </template>
  </div>
</template>

<script>
export default {
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
    }
  }
}
</script>

<style>

</style>