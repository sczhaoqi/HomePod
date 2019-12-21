<template>
  <div id="app">
    <a-layout id="components-layout-demo-top-side">
      <a-layout-header class="header">
        <div class="logo" />
        <a-menu
          theme="dark"
          mode="horizontal"
          :defaultSelectedKeys="['1']"
          @click="toPath"
          :style="{ lineHeight: '64px' }"
        >
          <a-menu-item key="1">空间</a-menu-item>
          <a-menu-item key="2">导航2</a-menu-item>
          <a-menu-item key="3">导航3</a-menu-item>
        </a-menu>
      </a-layout-header>
      <a-layout-content style="padding: 0 50px">
        <a-layout style="padding: 24px 0; background: #fff">
          <a-layout-sider width="200" style="background: #fff">
            <a-menu
              :openKeys="openKeys"
              :selectedKeys="selectedKeys"
              mode="inline"
              :inlineCollapsed="$store.state.isCollapse"
              @click="select"
              @openChange="openChange"
            >
              <a-sub-menu v-for="item in menus" :key="item.name" :index="item.title">
                <span slot="title">
                  <a-icon :type="item.icon" />
                  <span>{{ item.title }}</span>
                </span>
                <a-menu-item
                  v-for="subItem in item.submenu"
                  :key="subItem.index"
                  :index="subItem.index"
                >
                  <router-link :to="subItem.path">{{ subItem.text }}</router-link>
                </a-menu-item>
              </a-sub-menu>
            </a-menu>
          </a-layout-sider>
          <a-layout-content :style="{ padding: '0 24px', minHeight: '280px' }">
            <router-view />
          </a-layout-content>
        </a-layout>
      </a-layout-content>
      <a-layout-footer style="text-align: center">
        <nav>
          <a-row>
            <a-col>
              Copyright © 2017-2019 sczhaoqi. All Rights Reserved.
              <span>&nbsp;赵祺&nbsp;版权所有</span>
            </a-col>
          </a-row>
          <a-row :gutter="8">
            <a-col>
              <a
                href="https://www.beian.gov.cn/portal/registerSystemInfo?recordcode=44030502001921"
                target="_blank"
                style="padding:0 20px 0 0"
              >粤公网安备 44030502001921</a>
              <a
                href="http://beian.miit.gov.cn"
                target="_blank"
                style="padding:0 0 0 20px"
              >粤ICP备18057738号-1</a>
            </a-col>
          </a-row>
        </nav>
      </a-layout-footer>
    </a-layout>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "赵祺",
      openKeys: [this.$route.path.substr(0, this.$route.path.lastIndexOf("/"))],
      selectedKeys: [
        this.$route.path.substr(this.$route.path.lastIndexOf("/"))
      ],
      rootSubmenuKeys: ["/home", "/about"],
      menus: [
        {
          title: "个人",
          icon: "contacts",
          name: "home",
          submenu: [
            { text: "主页", path: "/", index: "/home", icon: "inbox" },
            {
              text: "联动",
              path: "/g2plot",
              index: "/g2plot",
              icon: "compass"
            },
            { text: "关于", path: "/about", index: "/about", icon: "compass" }
          ]
        }
      ]
    };
  },
  methods: {
    toPath({ item, key, keyPath }) {
      console.log(key);
      switch (key) {
        case "1":
          window.location.href = "https://www.sczhaoqi.com/qzone";
          break;
        default:
          /* eslint-disable */
          debugger;
          this.$message.info("暂未开放");
      }
    },
    openChange(openKeys) {
      // 只展开一个子菜单
      const latestOpenKey = openKeys.find(
        key => this.openKeys.indexOf(key) === -1
      );
      if (this.rootSubmenuKeys.indexOf(latestOpenKey) === -1) {
        this.openKeys = openKeys;
      } else {
        this.openKeys = latestOpenKey ? [latestOpenKey] : [];
      }
    },
    select({ item, key, selectedKeys }) {
      // 选中项
      this.selectedKeys = [key];
    }
  }
};
</script>
<style>
#components-layout-demo-top-side .logo {
  width: 120px;
  height: 31px;
  background: rgba(255, 255, 255, 0.2);
  margin: 16px 28px 16px 0;
  float: left;
}
</style>
