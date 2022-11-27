<script setup>
import useAPI from '@/composables/useAPI'

const { activePage, pages, getEmployees } = useAPI()
const prevPage = async () => {
  if (activePage.value > 1) {
    activePage.value--
    await getEmployees()
  }
}
const nextPage = async () => {
  if (activePage.value < pages.value) {
    activePage.value++
    await getEmployees()
  }
}
const jumpPage = async (page) => {
  activePage.value = page
  await getEmployees()
}
</script>

<template>
  <div class="pagination">
    <button class="action" :disabled="activePage === 1" @click="prevPage">
      Prev
    </button>
    <button
      v-for="page in pages"
      :key="page"
      class="page"
      :class="page === activePage ? 'active' : ''"
      @click="jumpPage(page)"
    >
      {{ page }}
    </button>
    <button class="action" :disabled="activePage === pages" @click="nextPage">
      Next
    </button>
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
