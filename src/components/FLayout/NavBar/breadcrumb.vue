<template>
  <el-breadcrumb class="app-breadcrumb" :separator="separator">
    <transition-group name="breadcrumb">
      <el-breadcrumb-item v-for="(item,index) in levelList" :key="item.path">
        <!-- 若是最后一项则不需要带跳转功能 -->
        <span v-if="item.redirect==='noRedirect'||index==levelList.length-1" class="no-redirect" :style="{color:textColor}">{{ item.meta.title }}</span>
        <!-- 为了使用a标签自带的样式但是不需要其click的自带事件，因此使用.prevent限制其执行原生事件 -->
        <a v-else :style="{color:textColor}" @click.prevent="handleLink(item)">{{ item.meta.title }}</a>
      </el-breadcrumb-item>
    </transition-group>
  </el-breadcrumb>
</template>

<script>
import pathToRegexp from 'path-to-regexp'
export default {
  name: 'Breadcrumb',
  props: {
    separator: {
      type: String,
      default: '/'
    },
    fixHome: {
      type: Boolean,
      default: false
    },
    textColor: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      levelList: null
    }
  },
  // 监听当前路由，若发生改变则重新生成面包屑
  watch: {
    $route() {
      this.getBreadcrumb();
    }
  },
  created() {
    this.getBreadcrumb()
  },
  methods: {
    getBreadcrumb() {
      // this.$route.matched包含当前路由的所有嵌套路径片段的路由记录
      // 过滤出没有title的路由或者是不显示面包屑的路由
      let matched = this.$route.matched.filter(item => item.meta && item.meta.title)
      // 若第一项不是首页，则默认加上首页作为面包屑第一项
      const first = matched[0]
      if (!this.isHome(first) && this.fixHome) {
        matched = [{ path: '/home', meta: { title: 'Home' }}].concat(matched)
      }

      this.levelList = matched.filter(item => item.meta && item.meta.title && item.meta.breadcrumb !== false)
    },
    isHome(route) {
      const name = route && route.name
      if (!name) {
        return false
      }
      return name.trim().toLocaleLowerCase() === 'Home'.toLocaleLowerCase()
    },
    // 用来处理 url 中地址与参数
    pathCompile(path) {
      const { params } = this.$route;
      const toPath = pathToRegexp.compile(path)
      return toPath(params)
    },
    handleLink(item) {
      const { redirect, path } = item;
      if (redirect) {
        this.$router.push(redirect)
        return;
      }
      this.$router.push(this.pathCompile(path));
    }
  }
}
</script>

<style lang="scss" scoped>
.app-breadcrumb{
  display: inline-block;
  font-size: 14px;
  line-height: 50px;
  margin-left: 8px;
  .no-redirect {
    color: #97a8be;
    cursor: text;
  }
}
</style>