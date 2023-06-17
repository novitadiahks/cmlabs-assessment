<template>
  <div class="mt-8 flex items-center flex-wrap">
    <ul class="flex items-center">
      <li class="inline-flex items-center">
        <NuxtLink to="/" class="flex items-center gap-x-1 text-gray-600 hover:text-blue-500">
          <Icon icon="ic:round-home" />Home
        </NuxtLink>
        <Icon class="mx-2 text-gray-400" icon="mingcute:right-line" />
      </li>

      <li class="inline-flex items-center">
        <NuxtLink to="/" class="flex items-center gap-x-1 text-gray-600 hover:text-blue-500">
          Foods
        </NuxtLink>
        <Icon class="mx-2 text-gray-400" icon="mingcute:right-line" />
      </li>

      <li v-for="(breadcrumb, index) in breadcrumbs" :key="index" class="inline-flex items-center">
        <NuxtLink :to="breadcrumb.path" class="flex items-center gap-x-1 text-gray-400 hover:text-blue-500">
          {{ breadcrumb.label }}
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>


<script setup lang="ts">
import { Icon } from "@iconify/vue";
const apiData = ref([]);
const breadcrumbs = computed(() => {
  const route = useRoute();

  const breadcrumb = Object.entries(route.query).map(([key, value]) => ({
    label: value,
    path: `${route.path}?${key}=${value}`,
  }));

  // Menggabungkan data dari API dengan breadcrumb yang ada
  return [...breadcrumb, ...apiData.value];
});
</script>

<style scoped></style>
