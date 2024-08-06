<script setup>
import { ref, reactive, computed, defineProps } from 'vue'
import { computers } from './temp_data';
import PCComponent from './PCComponent.vue';

defineProps({
    initialPc: {
        type: Number,
        default: 0
  }
})

  
const globalData = reactive({data: computers});
const currentPcIndex = ref(0);
const currentPcObject = computed(() => globalData.data[currentPcIndex.value]);
const tmpSpecName = ref("");


function addComponentForCurrentPhone (name) {
    if(name === "" || name === undefined) {
        return;
    }
    console.log(currentPcIndex.value);
    console.log(globalData.data[currentPcIndex.value]);
    globalData.data[currentPcIndex.value].specs.push(name.toString());
    tmpSpecName.value = "";
}

function onSelectPcIndex (event) {
    currentPcIndex.value = event.target.value;
}

</script>

<template>
    <h1>
        PC manager
    </h1>
    <select v-model="currentPcIndex" @change="onSelectPcIndex">
      <option v-for="(pc, index) in globalData.data" :key="index" :value="index">
        {{ pc.name }}
      </option>
    </select>
    <div>
        <PCComponent :pc="currentPcObject" />
    </div>
    <div class="flex mt-10 space-x-2 items-center">
        <input v-model="tmpSpecName" class="bg-white text-black h-10 rounded-md outline-none" type="text">
        <button @click="addComponentForCurrentPhone(tmpSpecName)">
            add specs
        </button>
    </div>
</template>