<template>
  <div class="rounded mx-30 mt-30">
    <div class="flex justify-between">
      <div class="flex-col">
        <div class="flex items-center gap-20">
          <span>{{ serial_num }}</span>
          <span>{{ localTitle }}</span>
        </div>
        <div class="flex items-center gap-20 my-10">
          <span class="w-80">问题描述  | </span>
          <span v-if="localDescribe" class="w-150">{{ localDescribe }}</span>
          <span v-if="!localDescribe" class="w-150">此问卷没有描述</span>
        </div>
      </div>
      <div class="flex-col justify-center items-center">
        <div class="flex gap-10 ">
          <span>必答</span>
          <input type="checkbox" class="checkbox-sm" :disabled="true" v-model="localOptionChoose"/>
        </div>
        <div class="flex gap-10">
          <span v-if="localUnique">唯一</span>
        </div>
      </div>
    </div>
    <div class="divider"></div>
    <div class="flex-col p-5 overflow-y-auto h-60">
      <input type="file" class="file-input file-input-bordered w-full max-w-xs shadow-md" />
    </div>
    <div class="divider"></div>
  </div>

</template>

<script setup lang="ts">
import {defineEmits, ref, watch} from "vue";

const props = defineProps<{
  serial_num: number,
  title?: string,
  optionChoose:boolean
  describe: string,
  unique:boolean
}>()
const emits = defineEmits(['update:content']);

const localTitle = ref<string>(props.title || '');
const localOptionChoose = ref<boolean>(props.optionChoose);
const localDescribe = ref<string>(props.describe || '');
const localUnique = ref<boolean>(props.unique);
watch(() => props.title, (newTitle) => {
  localTitle.value = newTitle || '';
});

watch(() => props.optionChoose, (newOptionChoose) => {
  localOptionChoose.value = newOptionChoose;
});

watch(() => props.unique, (newUnique) => {
  localUnique.value = newUnique;
});

watch(() => props.describe, (newLocalDescribe) => {
  localDescribe.value = newLocalDescribe
});

watch(localTitle, (newTitle) => {
  emits('update:title', newTitle);
});

</script>


<style scoped>

</style>