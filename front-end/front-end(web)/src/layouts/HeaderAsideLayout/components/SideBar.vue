<template>
  <scroll-bar>
    <div class="logo">
      
      <span class="site-name">通了后台</span>
    </div>
    <el-menu
      :show-timeout="200"
      mode="vertical"
      background-color="#00142a"
      text-color="hsla(0, 0%, 100%, .65)"
      active-text-color="#409EFF"
    >
      <template v-for="item in asideMenuConfig">
        <router-link
          v-if="!item.children"
          :to="item.path"
          :key="item.name">
          <el-menu-item :index="item.path">
            <i
              v-if="item.icon"
              :class="item.icon" />
            <span
              v-if="item.name"
              slot="title">{{ item.name }}</span>
          </el-menu-item>
        </router-link>

        <el-submenu
          v-else
          :index="item.name || item.path"
          :key="item.name">
          <template slot="title">
            <i
              v-if="item && item.icon"
              :class="item.icon" />
            <span
              v-if="item && item.name"
              slot="title">{{ item.name }}</span>
          </template>
          <template
            v-for="child in item.children"
            v-if="!child.hidden">
            <router-link
              :to="item.path + child.path"
              :key="child.name">
              <el-menu-item :index="item.path + child.path">
                <span
                  v-if="child && child.name"
                  slot="title">{{ child.name }}</span>
              </el-menu-item>
            </router-link>
          </template>
        </el-submenu>
      </template>
    </el-menu>
  </scroll-bar>
</template>

<script>
import { asideMenuConfig } from '@/config/menu';
import ScrollBar from './ScrollBar';

export default {
  name: 'SideBar',
  components: { ScrollBar },
  props: {},
  data() {
    return {
      asideMenuConfig,
    };
  },
};
</script>

<style lang="scss" scoped>
.logo {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 64px;
  line-height: 64px;
  background: #002140;
  color: #fff;
  text-align: center;
  font-size: 20px;
  font-weight: 600;
  overflow: hidden;
}
.site-name {
  margin-left: 10px;
}
.sidebar-container {
  box-shadow: 2px 0 6px rgba(0, 21, 41, 0.35);
  transition: width 0.28s;
  width: 256px !important;
  height: 100%;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  z-index: 1001;
  overflow: hidden;
  a {
    display: inline-block;
    width: 100%;
  }
  .el-menu {
    padding-top: 16px;
    width: 100% !important;
    border: none;
  }
  .el-submenu .el-menu-item {
    min-width: 256px !important;
    padding-left: 48px !important;
    background-color: #000c17 !important;
    &:hover {
      color: #fff !important;
    }
  }
  .el-menu-item,
  .el-submenu .el-menu-item {
    &.is-active {
      background-color: #188fff !important;
      color: #fff !important;
    }
  }
  .el-submenu__title i {
    font-size: 16px;
    color: rgba(255, 255, 255, 0.65);
  }
}
</style>
