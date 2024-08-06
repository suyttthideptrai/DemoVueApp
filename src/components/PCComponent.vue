<template>
    <div class="pc-card">
      <h2>Model: {{ pc.name }}</h2>
      <p>Price: ${{ pc.price }}</p>
      <div v-bind:class="css.specs_container">
        <ul>
            <li v-for="spec in pc.specs" :key="spec">{{ spec }}</li>
        </ul>
      </div>
    </div>
  </template>
  
<script setup>
import { defineProps } from 'vue';
  
defineProps({
pc: {
    type: Object,
    required: true
}
});

const css = {
    name: "text-underline",
    price: "",
    specs_container: "bg-white text-black rounded-md overflow-y-scroll w-[200px] h-[200px]"
}
</script>
