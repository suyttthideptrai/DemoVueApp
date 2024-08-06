<script setup>
import { ref } from 'vue'

defineProps({
  msg: String
})

const count = ref(0);
const isOn = ref(true);
const rawHtml = "<h1>hihiahah</h1>";
const sampleAttribute = "100"
const NULL_VALUE = null;
const UNDEFINED_VALUE = undefined;
const isShow = true;
const objectOfAttrs = {
  id: 'container',
  class: 'bg-red-500 text-center'
};
const listItemCss = 'text-center bg-white text-lg rounded-lg text-black';
const toggledCss = listItemCss + ' h-20'
const items =  [
        { id: 1, text: 'Item 1' },
        { id: 2, text: 'Item 2' },
        { id: 3, text: 'Item 3' }
      ];
  


function toogleThisShit() {
  isOn.value = !isOn.value;
}
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
  </div>

  <div class="card">
    <button class="select-none" type="button" @click="toogleThisShit">toggle</button>
  </div>

  <p v-if="isShow"
    v-bind:class="isOn ? listItemCss : toggledCss"
  >Now you see me</p>

  <p v-bind:ez-binding="'ez-game'">Using text interpolation: {{ rawHtml }}</p>
  <p>Using v-html directive: <span v-html="rawHtml"></span></p>

  <div v-bind="objectOfAttrs">
    <span>Hello uốt</span>
  </div>

  <div>
    <ul>
      <li v-bind:class="listItemCss" v-for="item in items" :key="item.id">{{ item.text }}</li>
    </ul>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
