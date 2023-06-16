<template>
  <main>
    <Header />
    <div class="container flex justify-center">
      <div
        class="w-3/5"
        v-for="(meal, index) in mealdetails.meals"
        :key="index"
      >
        <Breadcrumbs />
        <h1
          class="h-28 text-4xl flex items-center border-b-2 border-neutral-100"
        >
          {{ meal.strMeal }}
        </h1>
        <p class="my-4 text-red-500 font-bold">{{ meal.strArea }} Culinary</p>
        <div class="flex gap-x-6">
          <div class="w-3/5">
            <img class="rounded-2xl" :src="meal.strMealThumb" alt="" />
          </div>
          <div class="w-2/5 flex flex-col gap-y-4">
            <h2 class="text-3xl">Instruction</h2>
            <p class="text-justify">
              {{ meal.strInstructions }}
            </p>
            <h2 class="text-3xl">Receipes</h2>
            <div class="div">
              <ul class="pl-4 list-disc text-justify">
                <li
                  v-for="(ingredient, index) in formatReceipes(meal)
                    .ingredients"
                  :key="index"
                >
                  {{ formatReceipes(meal).measures[index] }} {{ ingredient }}
                </li>
              </ul>
            </div>
          </div>
        </div>
        <div class="mt-8 flex flex-col items-center">
          <h2 class="text-3xl">Tutorials</h2>
          <div class="youtube-video my-6">
            <iframe
              class=""
              width="720"
              height="480"
              :src="convertToEmbedURL(meal.strYoutube)"
              frameborder="0"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen
            ></iframe>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
import { count } from "console";

const config = useRuntimeConfig();
const route = useRoute();
const { data: mealdetails } = await useFetch(
  `${config.public.apiBase}/api/json/v1/1/lookup.php?i=${route.query.id_meals}`
);
function formatReceipes(receipt: any) {
  const ingredients = [];
  const measures = [];
  for (let i = 1; i < 20; i++) {
    const ingredient = receipt[`strIngredient${i}`];
    const measure = receipt[`strMeasure${i}`];

    if (ingredient && measure) {
      ingredients.push(ingredient);
      measures.push(measure);
    }
  }
  return {
    ingredients,
    measures,
  };
}
function convertToEmbedURL(url: string) {
  const videoId = url.split("watch?v=")[1];
  return `https://www.youtube.com/embed/${videoId}`;
}
</script>

<style scoped></style>
