<template>
  <div class="mt-8 flex items-center flex-wrap">
    <ul class="flex items-center">
      <li class="inline-flex items-center">
        <NuxtLink
          to="/"
          class="flex items-center gap-x-1 text-gray-600 hover:text-blue-500"
        >
          <Icon icon="ic:round-home" />Home
        </NuxtLink>
        <Icon class="mx-2 text-gray-400" icon="mingcute:right-line" />
      </li>

      <li class="inline-flex items-center">
        <NuxtLink
          to="/"
          class="flex items-center gap-x-1 text-gray-600 hover:text-blue-500"
        >
          Foods
        </NuxtLink>
        <Icon class="mx-2 text-gray-400" icon="mingcute:right-line" />
      </li>

      <li class="inline-flex items-center" v-for="(breadcrumb, index) in breadcrumbs" :key="index">
        <NuxtLink
          :to="breadcrumb.to"
          class="flex items-center gap-x-1 text-gray-400 hover:text-blue-500"
        >
          {{ breadcrumb.text }}
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { Icon } from "@iconify/vue";
const route = useRoute();
const breadcrumbs = computed(() => {
  const segments = route.path.split("/").filter((segment) => segment);
  const breadcrumbs = segments.map((segment, index) => ({
    text: segment,
    to: `/${segments.slice(0, index + 1).join("/")}`,
  }));
  return breadcrumbs;
});
</script>

<style scoped></style>
