<script setup>
import { RouterLink, RouterView } from "vue-router";
import { useAuth } from "@/stores/auth";

const auth = useAuth();
</script>

<template>
  <header class="py-6 bg-gray-100 shadow">
    <div class="container px-4 mx-auto md:px-2">
      <nav class="flex justify-between gap-4">
        <div class="flex items-center gap-4">
          <h2 class="text-xl font-bold">
            <div
              class="inline-flex items-center justify-center w-6 h-6 text-center text-white bg-blue-600 rounded"
            >
              P
            </div>
            myParking
          </h2>

          <template v-if="auth.check">
            <RouterLink class="router-link" :to="{ name: 'parkings.active' }">
              Parkings
            </RouterLink>
            <RouterLink class="router-link" :to="{ name: 'vehicles.index' }">
              Vehicles
            </RouterLink>
          </template>
          <template v-else>
            <RouterLink class="router-link" :to="{ name: 'home' }">
              Home
            </RouterLink>
          </template>
        </div>
        <div class="flex items-center gap-4">
          <template v-if="auth.check">
            <RouterLink class="router-link" :to="{ name: 'profile.edit' }">
              Profile
            </RouterLink>
            <RouterLink
              class="router-link"
              :to="{ name: 'profile.change-password' }"
            >
              Change password
            </RouterLink>
            <button @click="auth.logout" class="router-link">Logout</button>
          </template>
          <template v-else>
            <RouterLink class="router-link" :to="{ name: 'login' }">
              Login
            </RouterLink>
            <RouterLink class="router-link" :to="{ name: 'register' }">
              Register
            </RouterLink>
          </template>
        </div>
      </nav>
    </div>
  </header>

  <div class="container px-4 pt-8 mx-auto md:px-2 md:pt-16">
    <RouterView />
  </div>
</template>
