<template>
  <div id="app">
    <div class="layout">
      <Layout>
        <Sider
          ref="side1"
          hide-trigger
          collapsible
          :collapsed-width="78"
          v-model="isCollapsed"
        >
          <div class="sysName">
            <img src="@/assets/imgs/logo.png" alt="" width="50px" height="50px">
            <span style="margin-left:10px;font-size:18px;vertical-align:20px;" v-if="!isCollapsed">话机管理</span> 
          </div>
          <Menu
            theme="dark"
            width="auto"
            :class="menuitemClasses"
            @on-select="turnUrl"
            :active-name="$route.name"
          >
            <MenuItem name="Home">
              <Icon type="ios-home-outline" />
              <span>首页</span>
            </MenuItem>
            <MenuItem name="About">
              <Icon type="ios-clipboard-outline" />
              <span>关于</span>
            </MenuItem>
          </Menu>
        </Sider>
        <Layout>
          <Header :style="{ padding: 0 }" class="layout-header-bar">
            <Icon
              @click.native="collapsedSider"
              :class="rotateIcon"
              :style="{ margin: '0 20px' }"
              type="md-menu"
              size="24"
            ></Icon>
          </Header>
          <router-view />
        </Layout>
      </Layout>
    </div>
  </div>
</template>
<script>
export default {
  computed: {
    rotateIcon() {
      return ["menu-icon", this.isCollapsed ? "rotate-icon" : ""];
    },
    menuitemClasses() {
      return ["menu-item", this.isCollapsed ? "collapsed-menu" : ""];
    },
  },
  data() {
    return {
      isCollapsed: false,
    };
  },
  methods: {
    collapsedSider() {
      this.$refs.side1.toggleCollapse();
    },
    turnUrl(name) {
      this.$router.push(name);
    },
  },
};
</script>

<style lang="scss">
body {
  width: 100%;
  height: 100%;
}
html {
  width: 100%;
  height: 100%;
}
#app {
  width: 100%;
  height: 100%;
}
.ivu-layout {
  width: 100%;
  height: 100%;
}
.layout {
  background: #f5f7f9;
  position: relative;
  overflow: hidden;
  width: 100%;
  height: 100%;
  .sysName{
    color: rgba(255,255,255,0.8);
    height: 50px;
    margin: 20px 0;
    text-align: center;
  }
}
.layout-header-bar {
  background: #fff !important;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
}
.layout-logo-left {
  width: 90%;
  height: 30px;
  background: #5b6270;
  border-radius: 3px;
  margin: 15px auto;
}
.menu-icon {
  transition: all 0.3s;
}
.rotate-icon {
  transform: rotate(-90deg);
}
.menu-item span {
  display: inline-block;
  overflow: hidden;
  width: 69px;
  text-overflow: ellipsis;
  white-space: nowrap;
  vertical-align: bottom;
  transition: width 0.2s ease 0.2s;
}
.menu-item i {
  transform: translateX(0px);
  transition: font-size 0.2s ease, transform 0.2s ease;
  vertical-align: middle;
  font-size: 16px;
}
.collapsed-menu span {
  width: 0px;
  transition: width 0.2s ease;
}
.collapsed-menu i {
  transform: translateX(5px);
  transition: font-size 0.2s ease 0.2s, transform 0.2s ease 0.2s;
  vertical-align: middle;
  font-size: 22px;
}
</style>
