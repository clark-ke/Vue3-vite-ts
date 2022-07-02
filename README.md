# Vue3-vite-ts

npm init vite@latest
cd vite-project
npm install 
npm run dev


App.vue
<template>
  <div>{{ message1 ? "message1存在值" : "message1没有值" }}</div>
  <div v-text="message1"></div>
  <div>{{ message2 + 1 }}</div>
  <div>{{ message3.split(",") }}</div>
  <div>{{ message3.split(",").map((v) => `map方法${v}`) }}</div>
  <div v-html="message4"></div>
  <!-- v-if注释掉节点 -->
  <div v-if="flag" v-text="message1"></div>
  <!-- v-show操作css display -->
  <div v-show="flag" v-text="message1"></div>
  <!-- v-else-if -->
  <div>
    <div v-if="flag2 == 'A'">A</div>
    <div v-else-if="flag2 == 'B'">B</div>
    <div v-else-if="flag2 == 'C'">C</div>
    <div v-else="flag2 == 'D'">D</div>
  </div>

  <div>name:{{ jsonData.name }}</div>
  <div>age:{{ jsonData.age }}</div>

  <!-- v-on：click 与 @ -->
  <div><button v-on:click="clickTap">123</button></div>
  <div><button @click="clickTap">123</button></div>

  <!-- 点击父级与子集关系 -->
  <div @click="clickParent">
    <button @click="clickTap">点击触发父级与子集</button>
  </div>
  <!-- 只触发子集事件 -->
  <div @click="clickParent">
    <button @click.stop="clickTap">使用.stop只触发子集</button>
  </div>
</template>

<script setup lang="ts">
import { assert } from "@vue/compiler-core";

import * as jsonData1 from "./assets/test.json";
const message1: string = "v-text";
const message2: number = 12;
const message3: string = "你好1,你好2,你好3";
const message4: string = "<section>v-html渲染标签</section>";

const flag: boolean = true;
const flag2: String = "D";

const jsonData = jsonData1;

const clickTap = () => {
  console.log("触发了点击事件");
};

const clickParent = () => {
  console.log("点击了父级");
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
