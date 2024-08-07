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
        <PCComponent :pc="currentPcObject" 
        :removeSpecsForThisPC="removeSpecsForCurrentPC" 
        :updateSpecsValue="changeSpecsValue"
        />
    </div>
    <div class="flex mt-10 space-x-2 items-center">
        <input v-model="tmpSpecName" class="bg-white text-black h-10 rounded-md outline-none" type="text">
        <button @click="addComponentForCurrentPC(tmpSpecName)">
            add specs
        </button>
    </div>
</template>

<script setup>
import { ref, reactive, computed, defineProps } from 'vue'
import { computers } from './temp_data';
import PCComponent from './PCComponent.vue';

//Tham so cho page
const props = defineProps(
    {
        initialPc: {
            type: Number,
            default: 0
        }
    }
)

 // Khai bao state 
const globalData = reactive({data: computers});
const currentPcIndex = ref(props.initialPc);
const currentPcObject = computed(() => globalData.data[currentPcIndex.value]);
const tmpSpecName = ref("");

// Them specs cho PC hien tai
function addComponentForCurrentPC (name) {
    if(name === "" || name === undefined) {
        return;
    }
    console.log(currentPcIndex.value);
    console.log(globalData.data[currentPcIndex.value]);
    globalData.data[currentPcIndex.value].specs.push(name.toString());
    tmpSpecName.value = "";
}

// Thay doi PC hien tai
function onSelectPcIndex (event) {
    currentPcIndex.value = event.target.value;
}

// Thay doi gia tri specs
function changeSpecsValue (oldSpec, newSpec) {
    console.log(oldSpec + newSpec);
    globalData.data[currentPcIndex.value].specs = globalData.data[currentPcIndex.value].specs.map((item) => item === oldSpec ? newSpec : item);
}

// Xoa specs cho PC hien tai
function removeSpecsForCurrentPC (spec) {
    const index = globalData.data[currentPcIndex.value].specs.indexOf(spec);
    console.log(index);
    if (index !== -1) {
        globalData.data[currentPcIndex.value].specs.splice(index, 1);
    }
}


</script>
