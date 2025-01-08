<template>
   <div class="flex h-screen">
      <div class="w-1/5 bg-gray-50 border-r shadow">
         <Sidebar />
      </div>
      <div class="w-4/5 p-3">
         <div class="border h-full flex flex-col  rounded">
            <div class="h-16 px-3 flex items-center border-b">
               <div class="border px-2 py-1 bg-gray-100 flex item-center justify-center rounded">
                  <i class="ri-global-line text-gray-500"></i>
                  <small class="text-xs text-gray-600 leading-0 mt-1 ml-1">https://testsite.smartbloks.site</small>
               </div>
            </div>
            <iframe class="w-full flex-1" :src="`/preview?title=${newTitle}`"></iframe>
         </div>
      </div>
   </div>
</template>

<script lang='ts' setup>
import {ref, watch} from "vue";
import { storeToRefs } from 'pinia'
import { useEditorStore } from '../store/editor';

import Sidebar from '../components/Sidebar.vue'

const editorStore = useEditorStore()

const { title } = storeToRefs(editorStore)
const newTitle = ref<string>('')

/**
  flickering fix -
  debounce the title so it doesn't reload the iframe on every input
*/
const debounceTitle = () => {
   setTimeout(() => {
    newTitle.value = title.value
  }, 700)
}

watch(title, () => debounceTitle(), { immediate: true })
</script>

<style lang='postcss' scoped></style>