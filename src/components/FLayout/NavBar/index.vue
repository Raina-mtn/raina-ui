<template>
  <div class="navbar" :style="{'background-color':navBgColor,color:navTextColor,navHeight:navHeight}">
    <!-- navbar左侧 -->
    <div style="display: flex;align-items: center;">
      <hamburger v-if="hasHambuger" :is-active="opened" class="hamburger-container" :svg-color="navTextColor" @toggleClick="toggleSideBar" />
      <breadcrumb v-if="hasBreadcrumb" class="breadcrumb-container" :text-color="navTextColor" />
      <slot name="navLeft" />
    </div>
    <slot name="navCenter" />
    <div class="right-menu" :style="{color:navTextColor}">
      <slot name="navRight" />
      <!-- 自定义组件 -->
      <el-dropdown v-if="hasAvatar" class="avatar-container" trigger="click">
        <div class="avatar-wrapper" :style="{color: navTextColor}">
          <el-avatar :src="avatar" size="small" style="margin-right:10px" />
          <span>{{ user.userName || 'default' }}</span>
          <i class="el-icon-caret-bottom" />
        </div>
        <el-dropdown-menu slot="dropdown">
          <slot name="dropdownItems" />
        </el-dropdown-menu>
      </el-dropdown>
    </div>
  </div>
</template>

<script>
import Breadcrumb from "./breadcrumb.vue";
import Hamburger from "./hamburger.vue";
export default {
  name: "Navbar",
  components: {
    Breadcrumb,
    Hamburger
  },
  props: {
    opened: {
      type: Boolean,
      default: true
    },
    hasHambuger: {
      type: Boolean,
      default: true
    },
    hasBreadcrumb: {
      type: Boolean,
      default: true
    },
    navBgColor: {
      type: String,
      default: ''
    },
    navTextColor: {
      type: String,
      default: ''
    },
    navHeight: {
      type: String,
      default: '52px'
    },
    hasAvatar: {
      type: Boolean,
      default: true
    },
    avatar: {
      type: String,
      default: require('../../assets/images/user.png')
    },
    user: {
      type: Object,
      default: () => {}
    }
  },
  methods: {
    toggleSideBar() {
      this.$emit("toggleSideBar");
    }
  }
}
</script>

<style lang="scss" scoped>
.navbar{
  display: flex;
  justify-content: space-between;
  box-shadow: 0 1px 4px rgba(15, 18, 20, 0.1);
  .hamburger-container {
    line-height: 46px;
    height: 100%;
    float: left;
    cursor: pointer;
    transition: background .3s;
    -webkit-tap-highlight-color:transparent;

    &:hover {
      background: rgba(0, 0, 0, .025)
    }
  }
  .right-menu{
    display: flex;
    align-items: center;
    .avatar-container{
      cursor: pointer;//光标样式
      margin: 0 20px;
      .avatar-wrapper{
        display: flex;
        align-items: center;
      }
    }
  }
}
</style>