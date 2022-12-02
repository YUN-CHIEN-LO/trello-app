<script setup>
const props = defineProps({
  id: String,
  title: String,
  content: String,
});
</script>

<template>
  <div class="block my-2 w-full py-2 px-3 bg-white overflow-hidden select-none">
    <div class="font-bold block">{{ title }}</div>
    <div class="text-ellipsis overflow-hidden">{{ content }}</div>
  </div>
</template>
