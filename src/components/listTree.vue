<template>
    <li class="node-tree" >        
                <span class="span"> {{ child.name }}
                    <span class="btn-grp">
                    <button :class="{active : visible}" v-if="child.type === 'folder'" @click="formShow = true" >+</button>
                    <button :class="{active : visible}" @click="remove(child.id)"> - </button>
                    </span>
                </span>
                <div class="form">
                    <div class="file-folder-container" v-if="formShow && !type">
                    <button @click="type = 'folder'">Folder</button>
                    <button @click="type = 'file'">File</button>
                    </div>
                    <div v-else>
                       <file-output v-model:formShow="formShow" v-bind="{type}" v-if="formShow"  @add="add($event,callback,child)" />
                   </div>
                </div>
                <template v-if="child.childrens?.length">
                   <NodeTree  @add-data="(payload, callback) => $emit('add-data',payload, callback)" @remove-data="(id) =>$emit('remove-data',id)"  :folders="child.childrens" />
                </template>
    </li>
</template>

<script setup> 
import NodeTree from '@/components/NodeTree.vue'
import {defineProps ,ref  ,defineEmits} from 'vue'
import FileOutput from '@/components/FileOutput.vue'
  defineProps({
    child: {
        children: Object,
        default: () =>{}
    }
    })
    const emit = defineEmits(['add-data', 'remove-data'])



const visible =  ref(false)
const formShow = ref(false)
const type = ref('')

function add(text,callback, child){
   const payload = {
      type : type.value,
      name: text,
      child
   }
   emit('add-data',payload ,() => {
     type.value = ''
     formShow.value = false
   })
}

function remove(id) {
   emit('remove-data',id)
}


</script>



<style scoped>
.btn-grp {
    display: none;
}
.btn-grp button{
    margin-right: 5px;
}
.span:hover  .btn-grp{
    display: block;
}
</style>