<script setup>
import { ref } from 'vue';
import { useFocus } from '@vueuse/core';
import { vOnClickOutside } from '@vueuse/components';
import { useStore } from '/src/stores';
const target = ref();
useFocus(target, { initialValue: true });

const newTitle = ref('');
const isEditing = ref(false);

const props = defineProps({
  id: String,
});
const store = useStore();
const { addTask } = store;

// 儲存任務後清空輸入框
const addTaskToCard = () => {
  addTask(props.id, newTitle.value);
  newTitle.value = '';
  isEditing.value = false;
};
</script>

<template>
  <!-- add new task -->
  <div class="my-3">
    <div
      v-if="!isEditing"
      @click="isEditing = true"
      class="bg-slate-200 p-2 hover:bg-slate-300 cursor-pointer text-slate-500"
    >
      + 點擊以新增任務
    </div>
    <textarea
      v-else
      ref="target"
      v-on-click-outside="() => (isEditing = false)"
      v-model="newTitle"
      @keydown.enter="addTaskToCard"
      class="block w-full resize-none p-2 h-10"
      placeholder="為這張卡片輸入標題"
    ></textarea>
  </div>
  <!-- add new task -->
</template>
