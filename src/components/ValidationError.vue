<script setup>
import { defineProps } from "vue";
const props = defineProps(["errors", "field"]);
</script>

<template>
  <ul
    v-if="props?.errors?.value?.[props.field]?.length"
    class="flex flex-col gap-1 text-red-600"
  >
    <li v-for="message in props.errors.value[props.field]" :key="message">
      {{ message }}
    </li>
  </ul>
</template>
