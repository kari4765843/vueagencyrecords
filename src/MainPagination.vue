<script setup>
  import { ref } from 'vue'
  const pages = ref(10)
  const activePage = ref(4)
  const prevPage = () => {
    if (activePage.value > 1) {
      activePage.value--
    }
  }
  const nextPage = () => {
    if (activePage.value < pages.value) {
      activePage.value++
    }
  }
</script>
s

<template>
  <div class="pagination">
    <button class="action" :disabled="activePage === 1" @click="prevPage">Prev</button>
    <button
      v-for="page in pages"
      :key="page"
      class="page"
      :class="page === activePage ? 'active' : ''"
      @click="activePage = page"
    >
      {{ page }}
    </button>
    <button class="action" :disabled="activePage === pages" @click="nextPage">Next</button>
  </div>
</template>

<style lang="postcss" scoped>
  .pagination {
    @apply flex justify-center gap-4;
    .action {
      @apply rounded-md bg-gray-400 p-3 font-medium text-blue-900 shadow-md hover:bg-gray-400 disabled:text-yellow-900 hover:disabled:bg-gray-400;
    }
    .page {
      @apply rounded-md bg-gray-400 p-3 font-medium text-blue-900 shadow-md hover:bg-gray-400;
      &.active {
        @apply bg-blue-900 text-gray-400 hover:bg-red-300;
      }
    }
  }
</style>
