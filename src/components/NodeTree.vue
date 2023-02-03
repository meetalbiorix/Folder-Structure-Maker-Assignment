<template>
    <ul class="tree-list"  v-for="child in folders" :key="child.id">
        <list-tree @add-data="(payload,callback) => $emit('add-data',payload,callback)" @remove-data="(id) =>$emit('remove-data',id)" :child="child"></list-tree>
     </ul>   
</template>

<script>
  export default {
    name: 'NodeTree',
    inheritAttrs: false,
    customOptions: {}
  }
</script>

<script setup>
import {defineProps , defineEmits  } from 'vue'
import ListTree from '@/components/listTree.vue'


defineEmits(['add-data', 'remove-data'])

defineProps({
    folders: {
        children: Array,
        default: () =>[],
        id: String,
        name: String
    }
})


</script>

