<script setup>
import { onMounted } from "vue";
import { useVehicle } from "@/stores/vehicle";

const store = useVehicle();

onMounted(store.getVehicles);
</script>

<template>
  <div class="flex flex-col w-full mx-auto md:w-96">
    <h1 class="mb-4 text-2xl font-bold text-center">My vehicles</h1>

    <RouterLink
      :to="{ name: 'vehicles.create' }"
      class="w-full btn btn-primary"
    >
      Add vehicle
    </RouterLink>

    <div class="border-t h-[1px] my-6"></div>

    <div class="flex flex-col gap-2">
      <div
        v-for="vehicle in store.vehicles"
        :key="vehicle.id"
        class="flex justify-between w-full p-2 bg-gray-100"
      >
        <div class="flex items-center w-full overflow-hidden">
          <div class="text-xl plate">
            {{ vehicle.plate_number }}
          </div>
          <div class="pl-2 font-normal text-gray-600 truncate grow">
            {{ vehicle.description }}
          </div>
        </div>
        <div class="flex gap-1">
           <RouterLink
                :to="{ name: 'vehicles.edit', params: { id: vehicle.id } }"
                class="text-sm btn btn-secondary"
                >
                Edit
          </RouterLink>
          <button
            type="button"
            class="text-sm text-white bg-red-600 btn hover:bg-red-500"
          >
            X
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
