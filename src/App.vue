<script setup lang="ts">
import DarkModeButton from "./components/DarkModeButton.vue";
//import DarkModeSwitch from "./components/DarkModeSwitch.vue";

const isDarkModeEnabled = defineModel();
isDarkModeEnabled.value = false;

function onSwitched(isSwitched) {
  console.log("dark mode is enabled :", isSwitched);
}

let css_dict_ = {
  darkmode: {
    background: "#606060",
    color: "#ffffff",
  },
  lightmode: {
    background: "#ffffff",
    color: "#000000",
  },
};

let css_dict = {
  darkmode: {
    background: "red",
    color: "#ffffff",
  },
  lightmode: {
    background: "lightblue",
    color: "#000000",
  },
};


let cssvar_dict = {
  darkmode: [
    { name: "--main-background", value: "green" },
    { name: "--main-color", value: "red" },
  ],
  lightmode: [
    { name: "--main-background", value: "yellow" },
    { name: "--main-color", value: "blue" },
  ],
};
</script>

<template>
<h2> ## basic ## </h2>
  <DarkModeButton document_id="doc1" />
  <div id="doc1">
    <div>
      <h2>TEST TEST</h2>
    </div>

    <table border="1" style="background-color: lightgray">
      <thead>
        <tr>
          <th></th>
          <th>列-A</th>
          <th>列-B</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>行-1</th>
          <td>A-1</td>
          <td>B-1</td>
        </tr>
        <tr>
          <th>行-2</th>
          <td>A-2</td>
          <td>B-2</td>
        </tr>
        <tr>
          <th>行-3</th>
          <td>A-3</td>
          <td>B-3</td>
        </tr>
      </tbody>
    </table>
  </div>
<hr/>
<h2> ## model="model1" ## </h2>
  <DarkModeButton document_id="doc2" model="model1" />
  <div id="doc2">
    <p>AAAAAA</p>
    <p>AAAAAA</p>
    <p>AAAAAA</p>
  </div>
<hr/>
<h2>  :style_css  </h2>
  <DarkModeButton document_id="doc3" :style_css="css_dict" />
  <div id="doc3">
    <p>AAAAAA</p>
    <p>AAAAAA</p>
    <p>AAAAAA</p>
  </div>

<hr/>
<h2>  :css_var  </h2>
  <DarkModeButton document_id="doc4" :css_var="cssvar_dict" />
  <div id="doc4" class="target-element">
    <p>AAAAAA</p>
    <p>AAAAAA</p>
    <p>AAAAAA</p>
  </div>
<!--
<DarkModeSwitch @switched="onSwitched" v-model="isDarkModeEnabled"/>
-->
</template>

<style scoped>
:root {
  --main-background: yellow;
  --main-color: blue;
  --my-radius: 30px;
  --font-size: 16px;
  --main-height: 250px;
  --main-gutter: 30px;

}
.target-element {
  background: var(--main-background);
  /* border-radius: calc(var(--main-radius) * 2);*/
  border-radius: var(--my-radius);
  border: 2px solid red;

  color: var(--main-color);
  font-size: var(--font-size);
  height:var(--main-height);
  height:250px;
  margin: var(--main-gutter);
  /*margin: 30px;*/

}
</style>
