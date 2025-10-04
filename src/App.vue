<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import DarkModeButton from './components/DarkModeButton.vue'
import DarkModeSwitch from './components/DarkModeSwitch.vue'

const isDarkModeEnabled = defineModel()
isDarkModeEnabled.value = false;

function onSwitched(isSwitched) {
  console.log('dark mode is enabled :', isSwitched);
}
</script>

<template>
  <div>
    <a href="https://vite.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
  
  <DarkModeButton  document_id="doc1"/>
  <div id="doc1">
      <p>AAAAAA</p>
      <p>AAAAAA</p>
      <p>AAAAAA</p>
  </div>
  
  <DarkModeButton  document_id="doc2"/>
  <div id="doc2">
      <p>AAAAAA</p>
      <p>AAAAAA</p>
      <p>AAAAAA</p>
  </div>
  <DarkModeButton  document_id="doc3"/>
  <div id="doc3">
      <p>AAAAAA</p>
      <p>AAAAAA</p>
      <p>AAAAAA</p>
  </div>
  <!--
  <DarkModeSwitch @switched="onSwitched" v-model="isDarkModeEnabled"/>
  -->
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
