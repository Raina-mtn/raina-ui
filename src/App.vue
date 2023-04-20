<template>
  <div id="app">
    <img
      alt="Vue logo"
      src="./assets/logo.png"
    >
  </div>
</template>

<script>
export default {
  name: 'App',
  components:{
  },
  data() {
    return {
      menu:[
        {
          path:'test1',
          meta:{title:'测试1'}
        },
        {
          path:'test2',
          meta:{title:'测试2'},
          children:[
            {
              path:'test3',
              meta:{title:'子菜单测试1'}
            },
            {
              path:'test4',
              meta:{title:'子菜单测试2'}
            },
          ]
        },
      ]
    }
  },  
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
