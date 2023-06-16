<template>
  <main>
    <Header />
    <div class="container flex justify-center">
      <div class="w-3/5">
        <Breadcrumbs />
        <h1
          class="h-28 text-4xl flex items-center border-b-2 border-neutral-100"
        >
          {{ route.query.cat_name }}
        </h1>
        <div
          class="mt-6 flex flex-wrap justify-center justify-items-start gap-8"
        >
          <div class="" v-for="(cat, index) in catdetails.meals" :key="index">
            <NuxtLink
              :to="{
                path: '/mealdetails',
                query: { id_meals: cat.idMeal },
              }"
            >
              <button
                :style="{ 'background-image': `url(${cat.strMealThumb})` }"
                class="relative bg-cover bg-center w-40 h-32 rounded-2xl"
              >
                <div
                  class="absolute inset-0 flex items-center justify-center bg-black/30 hover:bg-black/40 rounded-2xl text-white font-bold"
                >
                  {{ cat.strMeal }}
                </div>
              </button>
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
const config = useRuntimeConfig();
const route = useRoute();
const { data: catdetails } = await useFetch(
  `${config.public.apiBase}/api/json/v1/1/filter.php?c=${route.query.cat_name}`
);
</script>

<style scoped></style>
