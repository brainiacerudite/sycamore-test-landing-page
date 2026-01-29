<template>
  <UPageSection
    class="mt-10 bg-white border-y border-black/15"
    :ui="{ container: 'py-0! relative xl:px-0!' }"
  >
    <div
      class="absolute inset-0 flex items-center justify-center pointer-events-none overflow-hidden"
      v-motion
      :initial="{ y: 50, opacity: 0 }"
      :visible="{ y: 0, opacity: 1, transition: { duration: 1500 } }"
    >
      <img src="/vector-map.svg" alt="map" class="absolute" />
    </div>

    <!-- Counter Content -->
    <UContainer>
      <div ref="counterSection" class="relative z-10 py-19.5">
        <div class="grid gap-8 md:grid-cols-3 md:gap-2 md:justify-between">
          <div
            v-for="(stat, index) in stats"
            :key="index"
            class="text-center md:text-left"
          >
            <div class="mb-4">
              <h2 class="text-4xl lg:text-[56px] font-bold text-staco-teal">
                <span>{{ Math.round(stat.currentValue.value) }}</span>
                <span v-if="stat.suffix" class="text-3xl lg:text-[40px]">{{
                  stat.suffix
                }}</span>
              </h2>
            </div>
            <p class="text-lg text-staco-teal">
              {{ stat.label }}
            </p>
          </div>
        </div>
      </div>
    </UContainer>
  </UPageSection>
</template>

<script lang="ts" setup>
import { useElementVisibility, useTransition } from "@vueuse/core";

const counterSection = ref<HTMLElement | null>(null);

const statsData = [
  { target: 200, suffix: "", label: "Countries Worldwide" },
  { target: 156, suffix: "K", label: "Registered User" },
  { target: 23, suffix: "K", label: "Small & Big Companies" },
];

// Track visibility of the section to trigger the count up
const targetIsVisible = useElementVisibility(counterSection);

// Map stats to transition objects
const stats = statsData.map((stat) => {
  const source = ref(0);
  const output = useTransition(source, {
    duration: 2500,
    transition: [0.75, 0, 0.25, 1],
  });

  return {
    ...stat,
    source,
    currentValue: output,
  };
});

// Watch visibility to trigger animation
watch(targetIsVisible, (isVisible) => {
  if (isVisible) {
    stats.forEach((stat) => {
      stat.source.value = stat.target;
    });
  }
});
</script>
