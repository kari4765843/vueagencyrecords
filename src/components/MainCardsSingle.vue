<script setup>
import { ref } from 'vue'
import { faker } from '@faker-js/faker'
import useAPI from '@/composables/useAPI'
const { getDepartment } = useAPI()
const selectCard = () => {
  console.log(`${props.employee.name} selected`)
}
const props = defineProps({
  employee: {
    type: Object,
    required: true,
    default: () => {
      return {
        createdAt: '2022-01-01',
        departmentId: '123',
        email: 'john.doe@example.com',
        employeeId: '123',
        name: 'John Doe',
        quote: 'Really Cool quote',
        title: 'Position',
        updatedAt: '2022-01-01',
      }
    },
  },
})
const departmentResponse = await getDepartment(props.employee.departmentId)
const department = ref(departmentResponse)
</script>

<template>
  <div class="card" @click="selectCard">
    <div class="card-image">
      <img :src="faker.internet.avatar()" alt="" srcset="" />
    </div>
    <div class="card-details">
      <p class="card-details-name">{{ props.employee.name }}</p>
      <p class="card-details-job">
        {{ props.employee.title }}, {{ department.name }}
      </p>
      <p class="card-details-quote">"{{ props.employee.quote }}"</p>
    </div>
  </div>
</template>

<style scoped lang="postcss">
.card {
  @apply cursor-pointer overflow-hidden rounded-lg bg-red-200 p-9 shadow-md transition-transform duration-150 hover:scale-105 hover:shadow-2xl hover:shadow-gray-400;
  &-image {
    img {
      @apply mx-auto rounded-full object-contain;
    }
  }
  &-details {
    @apply flex flex-col gap-3 pt-7 text-center;
    &-name {
      @apply font-serif text-2xl tracking-widest text-blue-900;
    }
    &-job {
      @apply -mt-3 text-sm font-bold text-red-800;
    }
    &-quote {
      @apply pt-5 text-lg font-semibold italic text-blue-900;
    }
  }
}
</style>
