<template>
      <h1>FOLDER STRUCTURE</h1>
      <folder-structure />
</template>

<script setup>

import { ref, onMounted } from 'vue'
import FolderStructure from '@/components/FolderStructure.vue'

const count = ref(0)

onMounted(() => {
  console.log(`The initial count is ${count.value}.`)
})

</script>

<style scoped>

h1 {

  background: black;
  color: white;
  padding: 20px ;
  text-align: center;
}
button {
  color: white;
  background: black;
  border-radius: 5px;
  padding: 8px 16px;
  cursor: pointer;
}
</style>



