<template>
     <div :class="componentStyle.container">
          <input :disabled="!isEditable" type="text" v-model="newMsg" :class="componentStyle.input_specs">
          <div :class="componentStyle.container_button">
               <button :class="componentStyle.button_update" @click="handleUpdateSpecsAction">
                    u
               </button>
               <button :class="componentStyle.button_delete" @click="$emit('removeSpecs', initialMsg)">
                    x
               </button>
          </div>
     </div>
</template>

<script setup>
import { ref, defineProps } from 'vue';
const props = defineProps(
     {
          initialMsg:{
               type: String,
               required: true
          }
     },
     {
          handleUpdateSpecs: {
               type: Function,
               required: true
          },
     }
)

const isEditable = ref(false);
const newMsg = ref(props.initialMsg);

function handleUpdateSpecsAction() {
     if(isEditable.value) {
          props.handleUpdateSpecs(props.initialMsg, newMsg.value);
          console.log("new message: ", newMsg.value);
          isEditable.value = false;
     }else {
          isEditable.value = true;
     }
}

// tailwind style classes
const componentStyle = {
     input_specs: "bg-inherit text-black h-10 rounded-md outline-none",
     container: "bg-white text-black rounded-md flex h-10 items-center justify-between hover:bg-gray-200",
     container_button: "flex",
     button_delete: "bg-red-500 text-white rounded text-center w-5 h-5 hover:bg-red-700 items-center justify-center flex",
     button_update: "bg-yellow-500 text-white rounded text-center w-5 h-5 hover:bg-yellow-700 items-center justify-center flex"
}
</script>