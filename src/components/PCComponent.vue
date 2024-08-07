<template>
    <div class="pc-card">
      <h2>Model: {{ pc.name }}</h2>
      <p :class="css.price">Price: ${{ pc.price }}</p>
      <p :class="css.instruction">
        Click 'u' to start update, click 'u' again to save <br>
        and 'x' to remove the spec
      </p>
      <div v-bind:class="css.specs_container">
        <div>
            <SpecsItems v-for="(spec) in pc.specs" 
            :initialMsg="spec" 
            :handleUpdateSpecs="updateSpecsValue"
            @removeSpecs="removeSpecsForThisPC" />
        </div>
      </div>
    </div>
  </template>
  
<script setup>
import { defineProps } from 'vue';
import SpecsItems from './UI/SpecsItems.vue';

  
const props = defineProps({
pc: {
    type: Object,
    required: true
},
updateSpecsValue: {
    type: Function,
    required: true,
},
removeSpecsForThisPC: {
      type: Function,
      required: true,
    },
});

const css = {
    name: "text-underline",
    price: "text-green-500",
    specs_container: "bg-white text-black rounded-md overflow-y-scroll w-[300px] h-[200px]",
    instruction: "text-blue-500 font-italic py-5"
}
</script>
