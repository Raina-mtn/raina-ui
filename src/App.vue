<template>
  <div id="app">
    <img
      alt="Vue logo"
      src="./assets/logo.png"
    >
    <side-bar :menu="menu" style="width: 200px;height: 200px;" />
  </div>
</template>

<script>
import SideBar from '@/components/FLayout/SideBar/index.vue'
import imgUrl from '../src/assets/logo.png';
export default {
  name: 'App',
  components: {
    SideBar
  },
  data() {
    return {
      menu: [
        {
          path: 'test1',
          meta: { title: '测试1', icon: imgUrl }
        },
        {
          path: 'test2',
          meta: { title: '测试2', icon: 'img', imgUrl: imgUrl },
          children: [
            {
              path: 'test3',
              meta: { title: '子菜单测试1' }
            },
            {
              path: 'test4',
              meta: { title: '子菜单测试2' }
            }
          ]
        }
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
