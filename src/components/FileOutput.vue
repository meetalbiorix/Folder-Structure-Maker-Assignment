<template>
<div class="input-container">
    <div>
        <img class="file" v-if="type === 'file'" src="../assets/image/file-regular.svg" alt="">
        <img class="file" v-else src="../assets/image/folder-open-regular.svg" alt="">
    </div>
      <input type="text" @input="changeInput"  v-model="text" />
                   <button @click="add">✔</button>
                   <button @click="$emit('update:formShow', false)">✕</button>

      <div class="error" v-if="hasError">This field is required.</div>
                   </div>

</template>

<script setup> 
import { defineEmits ,ref ,defineProps} from 'vue'

const text = ref('')
const hasError = ref(false)
const emit = defineEmits(['add'])
    defineProps({
        formShow: Boolean,
        type: String
    })

function changeInput(e) {
    console.log('event tareget',!e.target.value)
        hasError.value =  !e.target.value
}


function add(){
    if(!text.value || hasError.value){
        hasError.value = true
        return
    }
 emit('add',text.value,() => {
    text.value = ''
 })

}

</script>