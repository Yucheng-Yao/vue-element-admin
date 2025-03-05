<template>
  <div class="first-sidebar">
    <!-- ✅ 汉堡菜单按钮（用于切换侧边栏） -->
    <div class="sidebar-toggle-btn">
      <hamburger id="hamburger-container" :is-active="sidebar.opened" class="hamburger-container" @toggleClick="toggleSideBar" />
    </div>

    <el-menu
      :default-active="firstActiveMenu"
      background-color="transparent"
      text-color="#5F6368"
      active-text-color="#409EFF"
    >
      <el-menu-item index="mail" @click="selectFirstLevel('mail')">
        <i class="el-icon-message" />
        <span> Mail </span>
      </el-menu-item>
      <el-menu-item index="chat" @click="selectFirstLevel('chat')">
        <i class="el-icon-chat-dot-round" />
        <span> Chat </span>
      </el-menu-item>
      <el-menu-item index="meet" @click="selectFirstLevel('meet')">
        <i class="el-icon-video-camera" />
        <span> Meet </span>
      </el-menu-item>
    </el-menu>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Hamburger from '@/components/Hamburger' // ✅ 引入汉堡菜单组件

export default {
  components: {
    Hamburger
  },
  data() {
    return {
      firstActiveMenu: 'mail' // 默认选中的一级菜单
    }
  },
  computed: {
    ...mapGetters(['sidebar']) // ✅ 获取侧边栏状态
  },
  methods: {
    toggleSideBar() {
      this.$store.dispatch('app/toggleSideBar') // ✅ 触发 Vuex 操作，切换侧边栏状态
    },
    selectFirstLevel(group) {
      this.firstActiveMenu = group
      this.$emit('change-group', group) // ✅ 通知父组件 Layout.vue
    }
  }
}
</script>

<style scoped>
.first-sidebar {
  width: 80px;
  background-color: hsl(235, 93%, 30%); /* ✅ 设置背景颜色 */
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center; /* ✅ 确保内容水平居中 */
  padding-top: 25px;
}

/* ✅ 汉堡菜单按钮 */
.sidebar-toggle-btn {
  width: 100%;
  display: flex;
  justify-content: center;
  margin-bottom: 25px; /* ✅ 调整按钮与菜单之间的间距 */
}

/* ✅ 菜单项 */
.first-sidebar .el-menu {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* ✅ 确保鼠标 hover 效果正确显示 */
.first-sidebar .el-menu-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 90px;
  width: 100%;
}

/* ✅ 菜单项 hover 效果 */
.first-sidebar .el-menu-item:hover {
  background-color: rgba(0, 0, 0, 0.05);
}

/* ✅ 调整图标大小和间距 */
.first-sidebar .el-menu-item i {
  margin-top: 20px;
  font-size: 26px;
}

/* ✅ 让文字适当向下 */
.first-sidebar .el-menu-item span {
  font-size: 13px;
  display: block;
}
.hamburger-container {
  width: 50px; /* ✅ 让按钮保持合适的大小 */
  height: 50px;
  line-height: 46px; /* ✅ 让图标居中 */
  display: flex;
  align-items: center;
  justify-content: center;
  float: left;
  cursor: pointer;
  transition: background .3s, transform .2s ease-in-out;
  -webkit-tap-highlight-color: transparent;
  background: #4A4A4A; /* ✅ 设置深灰色背景 */
  border-radius: 50%; /* ✅ 让按钮变成圆形 */

  &:hover {
    background: #5A5A5A; /* ✅ 悬停时变亮一点 */
    transform: scale(1.05); /* ✅ 轻微放大效果，增加交互感 */
  }
}

</style>
