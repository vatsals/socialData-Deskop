<template>
  <div>
    <div name="query">
      <pre>{{ queryData }}</pre>
      <div class="modalCloseDiv">
        <button class="buttonGenerate buttonGenerateDef modalClose queryBtn" v-on:click="runQry">Run</button>
        <button class="buttonGenerate buttonGenerateDef modalClose queryBtn" v-on:click="closeWdw">Close</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ipcRenderer } from 'electron';
const remote = require('electron').remote;

export default {
  created() {
    ipcRenderer.on('querydata', (event, arg) => {
      this.queryData = arg
    })
  },

  methods: {
    closeWdw: function() {
      let window = remote.getCurrentWindow();
      window.close();
    },

    runQry: function() {
      let window = remote.getCurrentWindow();
      window.close();
    },
  },

  data() {
    return {
      queryData: ''
    }
  }
}
</script>

<style>
</style>


