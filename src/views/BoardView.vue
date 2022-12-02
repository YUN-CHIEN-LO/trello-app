<script setup>
import { ref, computed } from 'vue';
import { useStore } from '/src/stores';
import draggable from 'vuedraggable';
const store = useStore();
const list = computed(() => store.lists);
const toggle = ref(false);
// 從 store 取得 currentEditTask
const currentEditTask = computed(() => store.currentEditTask);
</script>

<template>
  <div class="bg-emerald-700 h-[100vh] w-full block overflow-x-auto overflow-y-hidden">
    <div id="board-wrapper" class="h-full w-full p-4 block overflow-auto">
      <draggable
        :list="list"
        group="card"
        itemKey="id"
        ghost-class="opacity-30"
        class="flex flex-row items-start"
      >
        <!-- 原本的 Card -->
        <template #item="{ element }">
          <Card v-bind="element" />
        </template>
        <!-- AddNewCard -->
        <template #footer>
          <AddNewCard />
        </template>
      </draggable>
    </div>

    <!-- lightbox -->
    <!-- 判斷 currentEditTask.id 是否存在來決定燈箱顯⽰與否 -->
    <EditBox v-if="currentEditTask?.id" />
  </div>
</template>
