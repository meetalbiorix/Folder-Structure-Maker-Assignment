<template>
    <button @click="formShow = true" class="add-to-root"> Add folder to root</button>
    <node-tree @add-data="add"  @remove-data="remove" :folders="folders" ></node-tree>
    <file-output v-model:formShow="formShow" type="folder" v-if="formShow"  @add="addRoot" />
</template>

<script setup >
import {   ref } from 'vue'
import NodeTree from '@/components/NodeTree.vue'
import FileOutput from '@/components/FileOutput.vue'

const folders =  ref([])
const formShow = ref(false)

function addRoot(text,callback){
    console.log(text,'text')
    const payload = {
        name: text,
        type: 'folder',
        id: (Math.random() + 1).toString(36).substring(7),
        childrens : []
    }
    folders.value.push(payload)
    formShow.value = false
    callback()
    
}

function add(   payload , callback){
    let clone = null
    const  found = (arr) =>{
        let node =  arr.find((node) => node.id === payload.child.id)
        if(!node){
            for(let i = 0 ;i < arr.length ;i++){
                const result =   found(arr[i].childrens)
                if(result){
                    node = result
                    break
                }
            }
        }
        return node
    }
    clone = found(folders.value)
    if(!clone){
        alert('id not found')
        return
    }
    clone.childrens.push({
        id: (Math.random() + 1).toString(36).substring(7),
        name: payload.name,
        childrens: [],
        type: payload.type

    })
    callback()

}
function remove(id){
   const  found = (arr) =>{
        for(let i = 0 ; i < arr.length ;i++) {
            if(arr[i].id === id){
                arr.splice(i,1)
                return
            }
            found(arr[i].childrens)
        }
    }
    found(folders.value)
}

</script>
