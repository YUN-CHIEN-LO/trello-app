<script setup>
import { ref, computed } from 'vue';
import { useStore } from '/src/stores';
const store = useStore();
const list = computed(() => store.lists);
const toggle = ref(false);
// 從 store 取得 currentEditTask
const currentEditTask = computed(() => store.currentEditTask);
</script>

<template>
  <div class="bg-emerald-700 h-[100vh] w-full block overflow-x-auto overflow-y-hidden">
    <div id="board-wrapper" class="h-full w-full p-4 block overflow-auto">
      <div class="flex flex-row items-start">
        <!-- card -->
        <Card v-for="card in list" :key="card.id" v-bind="card" />
        <!-- card -->

        <!-- add new list -->
        <AddNewList />
        <!-- add new list -->
      </div>
    </div>

    <!-- lightbox -->
    <!-- 判斷 currentEditTask.id 是否存在來決定燈箱顯⽰與否 -->
    <EditBox v-if="currentEditTask?.id" />
  </div>
</template>
