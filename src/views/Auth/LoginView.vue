<script setup>
import { onBeforeUnmount } from "vue";
import { useLogin } from "@/stores/login";

const store = useLogin();

onBeforeUnmount(store.resetForm);
</script>

<template>
  <form @submit.prevent="store.handleSubmit" novalidate>
    <div class="flex flex-col w-full mx-auto md:w-96">
      <h1 class="mb-4 text-2xl font-bold text-center">Login</h1>
      <div class="flex flex-col gap-2 mb-4">
        <label for="email" class="required">Email</label>
        <input
          v-model="store.form.email"
          id="email"
          name="email"
          type="text"
          class="form-input"
          autofocus
          autocomplete="email"
          required
          :disabled="store.loading"
        />
        <ValidationError :errors="store.errors" field="email" />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label for="password" class="required">Password</label>
        <input
          v-model="store.form.password"
          id="password"
          name="password"
          type="password"
          class="p-1 bg-gray-100 border"
          autocomplete="current-password"
          required
          :disabled="store.loading"
        />
        <ValidationError :errors="store.errors" field="password" />
      </div>

      <div class="flex flex-col gap-2">
        <label class="flex items-center gap-2 hover:cursor-pointer">
          <input
            v-model="store.form.remember"
            type="checkbox"
            class="w-4 h-4"
            :disabled="store.loading"
          />
          <span class="select-none">Remember me</span>
        </label>
      </div>

      <div class="border-t h-[1px] my-6"></div>

      <div class="flex flex-col gap-2">
        <button type="submit" class="btn btn-primary" :disabled="store.loading">
          <IconSpinner class="animate-spin" v-show="store.loading" />
          Login
        </button>
      </div>
    </div>
  </form>
</template>
