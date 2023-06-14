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

      <div>[active parkings list]</div>
    </div>
  </template>
