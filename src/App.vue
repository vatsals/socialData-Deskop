<template>
  <div id="app">
    <keep-alive>
      <router-view class="routeBox" />
    </keep-alive>
  </div>
</template>

<script>
import Header from './components/layout/Header';
const { remote, ipcRenderer } = require("electron")
const { Menu } = remote

export default {
  name: "app",
  components: {
    Header
  },

  created() {
    this.initMenu();
  },

  methods: {
    initMenu() {
      const menu = Menu.buildFromTemplate([
        {
          label: "File",
          submenu: [
            {
              label: "Social",
              accelerator: "CmdOrCtrl+s",
              click: () => {
                this.$router.push({ path: '/'})
              }
            },
            {
              label: "Query",
              accelerator: "CmdOrCtrl+q",
              click: () => {
                this.$router.push({name: 'query'})
              }
            },
            {
              label: "About",
              accelerator: "CmdOrCtrl+a",
              click: () => {
                this.$router.push({name: 'about'})
              }
            },
            { type: "separator" },
            {
              label: "Quit",
              accelerator: "CmdOrCtrl+Q",
              click: () => {
                alert('Shutting the Application');
                let window = remote.getCurrentWindow();
                window.close();
              }
            }
          ]
        },
        {
          label: "Edit",
          submenu: [
            {
              label: "Settings",
              accelerator: "CmdOrCtrl+,",
              click: () => {
                ipcRenderer.send("toggle-settings");
              }
            },
            {
              label: "Quit",
              accelerator: "CmdOrCtrl+Q",
              click: () => {
                let window = remote.getCurrentWindow();
                window.close();
              }
            }
          ]
        }
      ]);
      Menu.setApplicationMenu(menu);
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Open+Sans|Roboto');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Open Sans', sans-serif !important;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}

.routeBox {
  width: 90%;
  margin: 3% 5% 10% 5%;
}
</style>
