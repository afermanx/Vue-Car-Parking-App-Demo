<script setup>
import { onBeforeUnmount } from "vue";
import { useParking } from "@/stores/parking";

const store = useParking();

store.getActiveParkings();

function poll(callback) {
  return setInterval(callback, 3000);
}
const interval = poll(store.getActiveParkings);

onBeforeUnmount(() => clearInterval(interval));
</script>

<template>
  <div class="flex flex-col w-full mx-auto md:w-96">
    <h1 class="mb-4 text-2xl font-bold text-center">Active parkings</h1>

    <RouterLink
      :to="{ name: 'parkings.create' }"
      class="w-full btn btn-primary"
    >
      Order parking
    </RouterLink>

    <div class="border-t h-[1px] my-6"></div>

    <div class="flex flex-col gap-1">
      <div
        v-for="parking in store.parkings"
        :key="parking.id"
        class="flex flex-col gap-1 p-2 border"
      >
        <div class="text-2xl plate">{{ parking.vehicle.plate_number }}</div>
        <div class="text-sm text-gray-600">
          {{ parking.vehicle.description }}
        </div>
        <div class="p-2 bg-gray-100">
          {{ parking.zone.name }}
          ({{ (parking.zone.price_per_hour / 100).toFixed(2) }} &euro;/h)
        </div>
        <div>
          <div class="font-bold uppercase">from</div>
          <span class="font-mono">{{ parking.start_time }}</span>
        </div>
        <div class="flex items-top">
          <span class="text-2xl font-bold text-blue-600">{{
            (parking.total_price / 100).toFixed(2)
          }}</span>
          <span class="pt-0.5">&nbsp;&euro;</span>
        </div>
        <button
          type="button"
          @click="store.stopParking(parking)"
          class="ml-auto uppercase btn btn-danger"
        >
          stop
        </button>
      </div>
    </div>
  </div>
</template>
