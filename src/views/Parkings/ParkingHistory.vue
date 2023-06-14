<script setup>
import { useParking } from "@/stores/parking";

const store = useParking();

store.getStoppedParkings();
</script>

<template>
  <div class="flex flex-col w-full mx-auto md:w-96">
    <h1 class="mb-4 text-2xl font-bold text-center">Parking history</h1>

    <div class="flex flex-col gap-1">
      <div
        v-for="parking in store.stoppedParkings"
        :key="parking.id"
        class="flex flex-col gap-1 p-2 border"
      >
        <div class="text-2xl plate">{{ parking.vehicle.plate_number }}</div>
        <div class="p-2 bg-gray-100">
          {{ parking.zone.name }}
          ({{ (parking.zone.price_per_hour / 100).toFixed(2) }} &euro;/h)
        </div>
        <div>
          <div class="font-bold uppercase">from</div>
          <span class="font-mono">{{ parking.start_time }}</span>
        </div>
        <div>
          <div class="font-bold uppercase">to</div>
          <span class="font-mono">{{ parking.stop_time }}</span>
        </div>
        <div class="flex items-top">
          <span class="ml-auto text-2xl font-bold">{{
            (parking.total_price / 100).toFixed(2)
          }}</span>
          <span class="pt-0.5">&nbsp;&euro;</span>
        </div>
        <RouterLink
  :to="{ name: 'parkings.show', params: { id: parking.id } }"
  class="uppercase btn btn-secondary"
>
  view details
</RouterLink>
      </div>
    </div>
  </div>
</template>
