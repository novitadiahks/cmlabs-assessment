<template>
  <main>
    <Header />
    <div class="container">
      <section class="h-40 flex flex-col items-center justify-center gap-y-3">
        <div class="text-red-600 flex">
          <Icon icon="bxs:bowl-hot" />
          <Icon icon="bxs:bowl-rice" />
          <Icon icon="ic:sharp-cookie" />
        </div>
        <p>mealapp API website</p>
        <h1 class="text-5xl font-bold">See All The Delicious Foods</h1>
      </section>
      <section class="my-16 flex justify-center">
        <div class="flex flex-wrap justify-center gap-4 w-7/12">
          <div
            class=""
            v-for="(post, index) in posts.categories"
            :key="index"
          >
            <NuxtLink
              :to="{
                path: '/catdetails',
                query: { cat_name: post.strCategory },
              }"
            >
              <button
                :style="{ 'background-image': `url(${post.strCategoryThumb})` }"
                class="relative bg-cover bg-center w-40 h-20 rounded-2xl"
              >
                <div
                  class="absolute inset-0 flex items-center justify-center bg-black/30 hover:bg-black/40 rounded-2xl text-white font-bold"
                >
                  {{ post.strCategory }}
                </div>
              </button>
            </NuxtLink>
          </div>
        </div>
      </section>
    </div>
  </main>
</template>

<script setup lang="ts">
import { Icon } from "@iconify/vue";
const config = useRuntimeConfig();
const { data: posts } = await useFetch(
  `${config.public.apiBase}/api/json/v1/1/categories.php`
);
</script>

<style scoped></style>
