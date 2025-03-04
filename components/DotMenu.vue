<template>
  <Menu :model="items" class="w-full md:w-60 h-screen py-4">
    <template #start>
      <span class="inline-flex items-center gap-1 px-2 py-2">
        <span class="text-xl font-semibold">Dotbase Coding Challenge</span>
      </span>
    </template>
    <template #submenulabel="{ item }">
      <span class="text-primary font-bold">{{ item.label }}</span>
    </template>
    <template #item="{ item, props }">
      <NuxtLink
        v-ripple
        class="flex items-center"
        :to="item.to"
        v-bind="props.action"
      >
        <span :class="item.icon" />
        <span>{{ item.label }}</span>
      </NuxtLink>
    </template>
    <template #end>
      <div
        class="relative overflow-hidden w-full border-0 bg-transparent flex items-start p-2 pl-4 hover:bg-surface-100 dark:hover:bg-surface-800 rounded-none cursor-pointer transition-colors duration-200"
      >
        <Avatar :label="initials" class="mr-2" shape="circle" size="large" />
        <span class="inline-flex flex-col items-start">
          <span class="font-bold">
            {{ user.firstName }} {{ user.lastName }}
          </span>
          <span class="text-sm">{{ user.role }}</span>
        </span>
      </div>
    </template>
  </Menu>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

interface User {
  firstName: string;
  lastName: string;
  role: string;
}

interface Props {
  user: User;
}

const { user } = defineProps<Props>();

const initials = computed(() => `${user.firstName[0]}${user.lastName[0]}`);

const items = ref([
  { separator: true },
  {
    items: [
      { label: "Home", icon: "pi pi-home", to: "/" },
      { label: "Teams", icon: "pi pi-users", to: "/teams" },
    ],
  },
  {
    label: "Profile",
    items: [{ label: "Settings", icon: "pi pi-cog", to: "/settings" }],
  },
  { separator: true },
]);
</script>
