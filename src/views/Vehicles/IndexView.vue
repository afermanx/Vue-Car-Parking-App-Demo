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

      <div>There will be our vehicles list.</div>
    </div>
  </template>
