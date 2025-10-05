<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import DarkModeButton from './components/DarkModeButton.vue'
import DarkModeSwitch from './components/DarkModeSwitch.vue'

const isDarkModeEnabled = defineModel()
isDarkModeEnabled.value = false;

function onSwitched(isSwitched) {
  console.log('dark mode is enabled :', isSwitched);
}

let css_dict_ = {
  darkmode: {
     background : "#606060",
     color: "#ffffff"
  },
  lightmode: {
     background : "#ffffff",
     color: "#000000"
  }
}

let css_dict = {
  darkmode: {
     background : "red",
     color: "#ffffff"
  },
  lightmode: {
     background : "lightblue",
     color: "#000000"
  }
}
let css_dict2 = {
  darkmode: {
  },
  lightmode: {
  }
}
let cssvar_dict = {
  darkmode: [
    { name : "--main-background", value : "green" },
    { name : "--main-color"     , value : "red" }
  ],
  lightmode: [
    { name : "--main-background", value : "yellow" },
    { name : "--main-color"     , value : "blue" }
  ]
}
</script>

<template>
<DarkModeButton  document_id="doc1"/>
  <div id="doc1">
      <p>AAAAAA</p>
      <p>AAAAAA</p>
         <div>
	   <h2>TEST TEST</h2>
         </div>

         <table border="1" style="background-color:lightgray;">
            <thead>
              <tr><th></th><th>列-A</th><th>列-B</th></tr>
            </thead>
            <tbody>
              <tr><th>行-1</th><td>A-1</td><td>B-1</td></tr>
              <tr><th>行-2</th><td>A-2</td><td>B-2</td></tr>
              <tr><th>行-3</th><td>A-3</td><td>B-3</td></tr>
            </tbody>
         </table>
        
      <p>AAAAAA</p>
  </div>
  
<DarkModeButton  document_id="doc2" model="model1"/>
  <div id="doc2">
      <p>AAAAAA</p>
      <p>AAAAAA</p>
      <p>AAAAAA</p>
  </div>
  <DarkModeButton  document_id="doc3" :style_css="css_dict"/>
  <div id="doc3">
      <p>AAAAAA</p>
      <p>AAAAAA</p>
      <p>AAAAAA</p>
  </div>

  <DarkModeButton  document_id="doc4"  :css_var="cssvar_dict"/>
  <div id="doc4" class="target-element">
      <p>AAAAAA</p>
      <p>AAAAAA</p>
      <p>AAAAAA</p>
  </div>
<!--
<DarkModeSwitch @switched="onSwitched" v-model="isDarkModeEnabled"/>
-->
</template>

<style >

:root {
    --main-background: yellow;
    --main-color: blue;
    --font-size: 16px;
}
.target-element {
    background: var(--main-background);
    color: var(--main-color);
    font-size: var(--font-size);
}

</style>
