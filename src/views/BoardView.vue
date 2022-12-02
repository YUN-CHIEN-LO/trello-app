<script setup>
import { ref, computed } from 'vue';
import { useStore } from '/src/stores';
const store = useStore();
const list = computed(() => store.lists);
const toggle = ref(false);
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
    <div v-if="toggle" class="fixed top-0 left-0 w-full h-full bg-slate-800 z-100 bg-opacity-70">
      <div class="w-1/2 h-auto block relative mx-auto top-[15vh] bg-white py-8 px-12">
        <div>
          <input ref="target" type="text" class="w-full p-2 text-xl border mb-6" />
        </div>

        <textarea
          class="w-full h-[300px] p-3 overflow-x-hidden overflow-y-auto resize-none border"
        ></textarea>

        <div class="text-right mt-4">
          <button class="border bg-rose-500 text-white py-2 px-4 hover:bg-rose-700 mr-6">
            刪除
          </button>
          <button class="border bg-slate-200 py-2 px-4 hover:bg-slate-400 hover:text-slate-100">
            儲存送出
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
