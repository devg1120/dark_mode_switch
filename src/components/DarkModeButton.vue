<script lang="ts">
let cssvar_dict_default = {
  darkmode: [
  ],
  lightmode: [
  ] 
} ;

</script>
<script setup lang="ts">
import { ref, onMounted } from "vue";

//import cssToggle from "@/assets/css-toggle.yaml";
import cssToggle1 from "@/assets/css-toggle1.yaml";
import cssToggle2 from "@/assets/css-toggle2.yaml";

import cssElement from "@/assets/css-element.yaml";
import { IconSunFilled } from "@tabler/icons-vue";
import { IconMoonFilled } from "@tabler/icons-vue";
import { IconMoon } from "@tabler/icons-vue";

/*
const props = defineProps({
    model: { type: String, default: 'model2'},
    document_id: String,
    style_css:  { type: Object, default: cssElement},
    css_var:  { type: Object, default: cssvar_dict_default}
});
*/

const props = defineProps({
    model: { type: String, default: 'model2'},
    document_id: String,
    style_css:  { type: Object, default: cssElement},
    css_var:  { type: Object }
});

let doc = null;
const toggle_ele = ref();
const checkbox_id = "checkbox_" + props.document_id;

//let toggle_color = "model1"
let toggle_color = props.model;

let toggle_color_css = null;

if (toggle_color == "model1") {
  toggle_color_css = cssToggle1;
} else if (toggle_color == "model2") {
  toggle_color_css = cssToggle2;
}


onMounted(() => {
  doc = document.getElementById(props.document_id);
  darkmode.value = false;
  disableDarkMode();
});


const darkmode = ref(false);

function enableDarkMode() {
    darkmode.value = true;
    for (let [key, value] of Object.entries(toggle_color_css.darkmode)) {
      toggle_ele.value.style.setProperty(`--${key}`, value);
    }
if (!props.css_var) {
    for (let [key, value] of Object.entries(props.style_css.darkmode)) {
      doc.style.setProperty(key, value);
    }
} else {
    for (let i = 0; i < props.css_var.darkmode.length; i++  ) {
        let key = "";
        let value = "";
        for (let [k, v] of Object.entries(props.css_var.darkmode[i])) {
	   if ( k == "name"  ) { key = v   ; continue }
	   if ( k == "value" ) { value = v ; continue }
	}
	//console.log("setProperty", key, value);
        doc.style.setProperty(key, value);
    }
}
  }

function disableDarkMode() {
    darkmode.value = false;
    for (let [key, value] of Object.entries(toggle_color_css.lightmode)) {
      toggle_ele.value.style.setProperty(`--${key}`, value);
    }
if (!props.css_var) {
    for (let [key, value] of Object.entries(props.style_css.lightmode)) {
      doc.style.setProperty(key, value);
    }
} else {
    for (let i = 0; i < props.css_var.lightmode.length; i++  ) {
        let key = "";
        let value = "";
        for (let [k, v] of Object.entries(props.css_var.lightmode[i])) {
	   if ( k == "name"  ) { key = v   ; continue }
	   if ( k == "value" ) { value = v ; continue }
	}
	//console.log("setProperty", key, value);
        doc.style.setProperty(key, value);
    }
}
  }

</script>

<template>
  <div class="container" ref="toggle_ele">
    <input
      @change="darkmode ? disableDarkMode() : enableDarkMode()"
      :id="checkbox_id"
      type="checkbox"
      class="checkbox"
    />
    <label :for="checkbox_id" class="label transition">
      <IconMoonFilled v-if="toggle_color == 'model1'" class="icon" style="color:#ffffff;"/>
      <IconMoonFilled v-if="toggle_color == 'model2'" class="icon" style="color:#404040;"/>
      <IconSunFilled  class="icon" style="color:#404040;"/>
      <div :class="['toggle', 'transition', darkmode ? 'checked' : '']"></div>
    </label>
  </div>
</template>

<style scoped>
  .container {
    display: flex;
    justify-content: start;
    align-items: center;
    z-index: 100;
  }
  .checkbox {
    display: none;
  }
  .label {
    width: 40px;
    border-radius: 5px;
    border: 1px solid var(--text-color);
    padding: 3px 6px;
    background: var(--bg-dark-mode-toggle);
    cursor: pointer;
    display: flex;
    position: relative;
    justify-content: space-between;
    align-items: center;
  }
  .icon {
    font-size: 12px;
  }
  .toggle {
    position: absolute;
    background-color: var(--bg-secondary);
    border-radius: 3px;
    height: 20px;
    width: 20px;
    transform: translateX(0);
  }
  .toggle.checked {
    transform: translateX(20px) !important;
  }
  
  .transition {
    transition: all 0.8s ease;
    -webkit-transition: all 0.8s ease;
    -moz-transition: all 0.8s ease;
    -ms-transition: all 0.8s ease;
    -o-transition: all 0.8s ease;
  }
  
</style>

