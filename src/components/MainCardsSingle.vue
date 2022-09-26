<script setup>
  import { faker } from '@faker-js/faker'

  const firstName = faker.name.firstName()
  const lastName = faker.name.lastName()
  const fullName = `${firstName} ${lastName}`

  const selectCard = () => {
    console.log(`${fullName} selected`)
  }
</script>

<template>
  <div class="card" @click="selectCard">
    <div class="card-image">
      <img :src="faker.internet.avatar()" alt="" srcset="" />
    </div>
    <div class="card-details">
      <p class="card-details-name">{{ fullName }}</p>
      <p class="card-details-job">{{ faker.name.jobTitle() }}, {{ faker.name.jobArea() }}</p>
      <p class="card-details-quote">"{{ faker.lorem.paragraph() }}"</p>
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
