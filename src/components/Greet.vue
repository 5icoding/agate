<script setup>
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/tauri";

const greetMsg = ref("");
const name = ref("");

async function greet() {
  // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
  greetMsg.value = await invoke("greet", { name: name.value });
}

const helloMsg = ref("");
const helloName = ref("");

async function hello() {
  // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
  helloMsg.value = await invoke("hello", { name: helloName.value });
  
}
</script>

<template>
  <form class="row" @submit.prevent="greet">
    <input id="greet-input" v-model="name" placeholder="Enter a name..." />
    <button type="submit">Greet</button>
  </form>

  <p>{{ greetMsg }}</p>

  <form class="row" @submit.prevent="hello">
    <input id="hello-input" v-model="helloName" placeholder="Enter a ask..." />
    <button type="submit">提问</button>
  </form>
  <p>
    回答如下：
  </p>
  <p>{{ helloMsg }}</p>
</template>
