<script setup>
import { watchEffect, onBeforeUnmount } from "vue";
import { useParking } from "@/stores/parking";
import { useRoute } from "vue-router";

const store = useParking();
const route = useRoute();

watchEffect(async () => {
  store.getParking({ id: route.params.id });
});

onBeforeUnmount(store.resetParkingDetails);
</script>

<template>
  <div
    class="flex flex-col w-full mx-auto md:w-96"
    v-if="store.parking.id !== undefined"
  >
    <h1 class="mb-4 text-2xl font-bold text-center">Parking order details</h1>

    <div class="p-2 font-mono border">
      <div class="mb-4 font-bold uppercase">
        parking order #{{ store.parking.id }}
      </div>

      <div class="font-bold uppercase">license plate</div>
      <div class="text-2xl plate">{{ store.parking.vehicle.plate_number }}</div>

      <div class="font-bold uppercase">description</div>
      <div>{{ store.parking.vehicle.description }}</div>

      <div class="font-bold uppercase">zone</div>
      <div>{{ store.parking.zone.name }}</div>

      <div class="font-bold uppercase">price</div>
      <div>
        {{ (store.parking.zone.price_per_hour / 100).toFixed(2) }} &euro; per
        hour
      </div>

      <div class="font-bold uppercase">from</div>
      <div>{{ store.parking.start_time }}</div>

      <div class="font-bold uppercase">to</div>
      <div>{{ store.parking.stop_time }}</div>

      <div class="font-bold uppercase">total</div>
      <div class="text-xl">
        {{ (store.parking.total_price / 100).toFixed(2) }} &euro;
      </div>
    </div>

    <div class="border-t h-[1px] my-6"></div>

    <RouterLink
      :to="{ name: 'parkings.history' }"
      class="uppercase btn btn-secondary"
    >
      return
    </RouterLink>
  </div>
</template>
