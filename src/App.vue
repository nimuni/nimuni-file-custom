<template>
  <v-app>
    <div>
      <v-toolbar color="purple darken-2" dense dark style="-webkit-app-region: drag;">
        <v-app-bar-nav-icon @click="drawer = true" style="-webkit-app-region: no-drag;"></v-app-bar-nav-icon>
        <v-toolbar-title>니무니파일커스텀앱</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn icon style="-webkit-app-region: no-drag;"><v-icon @click="minimize">mdi-minus</v-icon></v-btn>
        <v-btn icon style="-webkit-app-region: no-drag;"><v-icon @click="maxinize">mdi-checkbox-blank-outline</v-icon></v-btn>
        <v-btn icon style="-webkit-app-region: no-drag;"><v-icon @click="close">mdi-close</v-icon></v-btn>
      </v-toolbar>

      <v-navigation-drawer
        v-model="drawer"
        absolute
        temporary
        style="z-index:10;"
      >
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title>메뉴</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-divider></v-divider> 

        <v-list nav dense >
          <v-list-item-group
            v-model="group"
            active-class="deep-purple--text text--accent-4"
          >
            <v-list-item v-for="route in $router.options.routes" :key="route.path" :to="route.path">
              <v-list-item-icon>
                <v-icon>mdi-file</v-icon>
              </v-list-item-icon>
              <v-list-item-title>{{ route.name }}</v-list-item-title>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-navigation-drawer>
      <router-view />
    </div>
  </v-app>
</template>

<script>
const { ipcRenderer } = window.require("electron");
const remote = window.require('electron').remote;

import "./css/reset.css";
export default {
  name: 'App',

  data: () => ({
    drawer: false,
    group: null,
  }),
  methods: {
    minimize: function(){
      let window = remote.getCurrentWindow();
      window.minimize(); 
    },
    maxinize: function(){
      let window = remote.getCurrentWindow();
      if (!window.isMaximized()) {
          window.maximize();          
      } else {
          window.unmaximize();
      }
    },
    close: function(){
      let window = remote.getCurrentWindow();
      window.close();
    }
  }
};
</script>

<style>
/* delete y-scroll-bar */
::-webkit-scrollbar {
  display: none;
}
</style>