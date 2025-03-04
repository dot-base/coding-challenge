<template>
  <div class="flex min-h-screen bg-slate-100">
    <DotMenu :user="user" class="h-full" />

    <div class="flex-1 m-4 p-4 bg-white border border-slate-200 rounded">
      <DotBreadcrumb :home="home" :items="items" />
      <div class="px-4">
        <slot />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const route = useRoute();

const user = {
  firstName: "John",
  lastName: "Doe",
  role: "Admin",
};

const home = ref({
  icon: "pi pi-home",
  route: "/",
});

const items = computed(() => {
  if (route.path === '/settings') {
    return [{ label: "Settings", route: "/settings" }];
  }
  if (route.path === '/') {
    return [{ label: "Home", route: "/" }];
  }
  return [];
});
</script>
