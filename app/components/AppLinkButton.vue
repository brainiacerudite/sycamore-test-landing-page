<template>
  <ULink
    as="button"
    :to="to"
    :variant="variant"
    :size="size"
    class="relative rounded-full px-6 lg:px-8 py-4 font-bold text-white hover:text-staco-dark bg-staco-accent hover:bg-staco-green overflow-hidden group"
  >
    <span
      class="absolute inset-0 bg-staco-green translate-y-full group-hover:translate-y-0 transition-transform duration-300 ease-out"
    ></span>
    <span
      class="relative z-10 inline-block group-hover:-translate-y-0.5 transition-transform duration-300 ease-out"
    >
      <slot />
    </span>
  </ULink>
</template>

<script lang="ts" setup>
defineProps<{
  to: string;
  variant?: "solid" | "ghost" | "outline";
  size?: "sm" | "md" | "lg" | "xl";
  class?: string;
}>();
</script>
