<script setup>
  import { ref } from 'vue'
  import { useAuth } from './composables/useAuth'

  const { isAuthenticated, logout, user } = useAuth()

  const brand = ref('🏛️ Agency Records')
</script>

<template>
  <nav>
    <div class="Wrapper">
      <RouterLink :to="{ name: 'Home' }" class="brand">
        <span class="brand-title">{{ brand }}</span>
      </RouterLink>
      <div class="menu">
        <p v-show="isAuthenticated" class="px-2 py-4">
          Welcome back<strong
            ><i>{{ user.name }}</i></strong
          >
        </p>
        <div v-if="isAuthenticated">
          <RouterLink :to="{ name: 'Settings' }" href="#" class="menu-item">Settings</RouterLink>
          <Button class="menu-logout" @click="logout">Logout</Button>
        </div>
        <div v-else>
          <RouterLink :to="{ name: 'Login' }" href="#" class="menu-login">Login</RouterLink>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped lang="postcss">
  nav {
    @apply flex h-20  bg-yellow-900 text-rose-100;
    .Wrapper {
      @apply container mx-auto  flex w-full  items-center justify-between;
      .brand {
        &-title {
          @apply text-3xl font-semibold text-red-300;
        }
      }
      .menu {
        @apply flex gap-2;
        & div {
          @apply py-2;
        }
        &-item {
          @apply rounded-md px-4 py-2 hover:bg-red-600 hover:text-red-300;
        }
        &-login {
          @apply rounded-md bg-red-600 px-4 py-2 text-rose-100 hover:bg-yellow-800;
        }
        &-logout {
          @apply rounded-md bg-blue-800 px-3 py-3 text-rose-100 hover:bg-yellow-800;
        }
      }
    }
  }
</style>
