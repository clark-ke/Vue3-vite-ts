//npm init vite@latest

<template>
  <div>三元表达式:{{ message1 ? "message1存在值" : "message1没有值" }}</div>
  <div v-text="message1"></div>
  <div>运算模板值:{{ message2 + 1 }}</div>
  <div>split方法{{ message3.split(",") }}</div>
  <div>map方法{{ message3.split(",").map((v) => `map方法${v}`) }}</div>

  <div v-html="message4"></div>
  <br />
  <div>v-if与v-show的区别</div>
  <!-- v-if注释掉节点 -->
  <div v-if="flag" v-text="message1"></div>
  <!-- v-show操作css display -->
  <div v-show="flag" v-text="message1"></div>

  <br />
  <!-- v-else-if -->
  <div>
    <div>v-else用法</div>
    <div v-if="flag2 == 'A'">A</div>
    <div v-else-if="flag2 == 'B'">B</div>
    <div v-else-if="flag2 == 'C'">C</div>
    <div v-else="flag2 == 'D'">D</div>
  </div>
  <br />

  <br />
  <div>点击事件</div>
  <!-- v-on：click 与 @ -->
  <div><button v-on:click="clickTap">v-on:click触发点击</button></div>
  <div><button @click="clickTap">@click触发点击</button></div>
  <br />

  <!-- 点击父级与子集关系 -->
  <div @click="clickParent">
    <button @click="clickTap">点击触发父级与子级</button>
  </div>
  <!-- 只触发子集事件 -->
  <div @click="clickParent">
    <button @click.stop="clickTap">使用.stop只触发子级</button>
  </div>
  <br />
  <form>
    <button>提交刷新</button>
  </form>
  <form>
    <button @click.prevent="clickTap">提交 使用click.prevent不刷新1</button>
  </form>
  <br />
  <div v-bind:style="style">style效果1 v-bind绑定当前变量等于目标</div>
  <div :style="style">style效果2 使用 ":"简写v-vind绑定当前变量等于目标</div>
  <div :class="cls">样式控制</div>

  <br />
  <div>v-for迭代对象</div>
  <div v-for="item in arr">{{ item }}</div>

  <div>v-for嵌套迭代对象</div>
  <div :key:any="item" v-for="item in jsonData">
    {{ item }}
    <div :childKey:any="keyItem" v-for="keyItem in item">{{ keyItem }}</div>
    <div :childKey:any="keyItem" v-for="keyItem in item">
      {{ keyItem.name }}-{{ keyItem.age }}
    </div>
  </div>
  <br />
  <div>v-model双向绑定</div>
  <div>使用vue.ref包装属性变成响应式</div>
  <input v-model="message5" type="text" />
  <div>{{ message5 }}</div>

  <div>{{ proxyObj.color }}</div>
</template>

<script setup lang="ts">
import { assert } from "@vue/compiler-core";
import { ref } from "vue";

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

type Style = {
  color: string;
  height: string;
};
const style: Style = { color: "blue", height: "50px" };

type Cls = {
  a: boolean;
  b: boolean;
};

const cls: Cls = {
  a: true,
  b: true,
};

const arr: Array<string> = ["A", "B", "C", "D", "E"];

// splice用法
arr.splice(2, 1, "ffff");

const message5 = ref("test");

let proxyObj = new Proxy(style, {
  get: function (target, prop) {
    return prop in target ? target[prop] : 0;
  },
  set: function (target, prop, value) {
    target[prop] = 888;
  },
});
</script>

<style>
.a {
  color: red;
}
.b {
  border: 2px solid aquamarine;
}

div {
  margin: 20px;
}
</style>
