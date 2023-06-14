<script setup>
import { onBeforeUnmount } from "vue";
import { useRegister } from "@/stores/register";

const store = useRegister();

onBeforeUnmount(store.resetForm);
</script>

<template>
  <form @submit.prevent="store.handleSubmit" novalidate>
    <div class="flex flex-col w-full mx-auto md:w-96">
      <h1 class="mb-4 text-2xl font-bold text-center">Register</h1>
      <div class="flex flex-col gap-2 mb-4">
        <label for="name" class="required">Name</label>
        <input
          :disabled="store.loading"
          v-model="store.form.name"
          id="name"
          name="name"
          type="text"
          class="form-input"
          autocomplete="name"
          required
        />
        <ValidationError :errors="store.errors" field="name" />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label for="email" class="required">Email</label>
        <input
          :disabled="store.loading"
          v-model="store.form.email"
          id="email"
          name="email"
          type="email"
          class="form-input"
          autocomplete="email"
          required
        />
        <ValidationError :errors="store.errors" field="email" />
      </div>

      <div class="flex flex-col gap-2 mb-4">
        <label for="password" class="required">Password</label>
        <input
          :disabled="store.loading"
          v-model="store.form.password"
          id="password"
          name="password"
          type="password"
          class="form-input"
          autocomplete="new-password"
          required
        />
        <ValidationError :errors="store.errors" field="password" />
      </div>

      <div class="flex flex-col gap-2">
        <label for="password_confirmation" class="required">
          Confirm password
        </label>
        <input
          :disabled="store.loading"
          v-model="store.form.password_confirmation"
          id="password_confirmation"
          name="password_confirmation"
          type="password"
          class="form-input"
          autocomplete="new-password"
          required
        />
      </div>

      <div class="border-t h-[1px] my-6"></div>

      <div class="flex flex-col gap-2">
        <button
        :disabled="store.loading" type="submit" class="btn btn-primary">
        <IconSpinner v-show="store.loading" />
        Register</button>
      </div>
    </div>
  </form>
</template>
