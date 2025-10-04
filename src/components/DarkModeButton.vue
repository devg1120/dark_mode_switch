<script setup>
import { ref, onMounted } from "vue";

import cssToggle from "@/assets/css-toggle.yaml";
import cssElement from "@/assets/css-element.yaml";
import { IconSunFilled } from "@tabler/icons-vue";
import { IconMoonFilled } from "@tabler/icons-vue";
import { IconMoon } from "@tabler/icons-vue";

const props = defineProps(['document_id'])

let doc = null;
const toggle_ele = ref();
const checkbox_id = "checkbox_" + props.document_id;

onMounted(() => {
  doc = document.getElementById(props.document_id);
  darkmode.value = false;
  disableDarkMode();
});


const darkmode = ref(false);

function enableDarkMode() {
    darkmode.value = true;
    for (let [key, value] of Object.entries(cssToggle.darkmode)) {
      toggle_ele.value.style.setProperty(`--${key}`, value);
    }
    for (let [key, value] of Object.entries(cssElement.darkmode)) {
      doc.style.setProperty(key, value);
    }
  }

function disableDarkMode() {
    darkmode.value = false;
    for (let [key, value] of Object.entries(cssToggle.lightmode)) {
      toggle_ele.value.style.setProperty(`--${key}`, value);
    }
    for (let [key, value] of Object.entries(cssElement.lightmode)) {
      doc.style.setProperty(key, value);
    }
  }

  // Initialise the dark mode depending on the user's preferences
  /*
  if (window?.matchMedia?.("(prefers-color-scheme:dark)")?.matches) {
    darkmode.value = true;
    enableDarkMode();
  } else {
    darkmode.value = false;
    disableDarkMode();
  }
  */
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
    <!--
      <span class="icon">🌙</span>
      <span class="icon">☀️</span>
      -->
      <IconMoonFilled class="icon" style="color:#ffffff;"/>
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

