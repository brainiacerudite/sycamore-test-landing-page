<template>
  <header
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-300 transform"
    :class="[
      isNavbarVisible ? 'translate-y-0' : '-translate-y-full',
      isScrolled
        ? 'bg-white/80 backdrop-blur-md shadow-sm'
        : 'bg-white lg:py-4 lg:bg-transparent',
    ]"
  >
    <UContainer>
      <div
        class="relative flex items-center justify-between h-20 lg:rounded-full transition-all duration-300"
      >
        <div
          class="absolute hidden inset-0 rounded-full transition-opacity duration-300 lg:block"
          :class="isScrolled ? 'opacity-0' : 'opacity-100'"
        >
          <div
            class="absolute inset-0 rounded-full bg-linear-to-b from-neutral-700 to-neutral-800 shadow-[0_8px_32px_rgba(0,0,0,0.6),0_2px_8px_rgba(0,0,0,0.4),inset_0_1px_0_rgba(255,255,255,0.1),inset_0_-1px_2px_rgba(0,0,0,0.5)]"
          ></div>
          <div
            class="absolute inset-0.75 rounded-full bg-linear-to-b from-neutral-800 to-neutral-900 shadow-[inset_0_2px_4px_rgba(0,0,0,0.8),inset_0_-1px_2px_rgba(255,255,255,0.05)]"
          ></div>
        </div>

        <div
          class="w-full flex items-center justify-between h-20 lg:px-4 lg:py-0 lg:absolute lg:rounded-full"
        >
          <div class="shrink-0">
            <ULink to="/" class="flex items-center gap-2">
              <AppLogo />
            </ULink>
          </div>

          <nav class="hidden lg:flex items-center relative">
            <div
              class="absolute h-10 bg-white/10 hover:bg-white/10 rounded-full transition-all duration-300 ease-out"
              :style="{
                left: `${indicatorLeft}px`,
                width: `${indicatorWidth}px`,
              }"
            ></div>
            <NuxtLink
              v-for="(link, index) in links"
              :key="link.label"
              :to="link.to"
              :ref="(el: any) => setTabRef(el, index)"
              @click="setActiveTab(index)"
              active-class="text-white font-semibold"
              class="relative z-10 text-[15px] font-medium text-gray-300 hover:text-white transition-colors px-6 py-2"
              :class="[
                activeTab === index
                  ? isScrolled
                    ? 'text-staco-dark font-bold'
                    : 'text-white font-bold'
                  : isScrolled
                    ? 'text-gray-500 hover:text-staco-dark'
                    : 'text-gray-300 hover:text-white',
              ]"
            >
              {{ link.label }}
            </NuxtLink>
          </nav>

          <div class="hidden lg:flex items-center gap-4">
            <ULink
              to="#"
              class="text-sm font-semibold hover:text-green-600 transition-colors"
              :class="isScrolled ? 'text-gray-700' : 'text-white'"
            >
              Sign in
            </ULink>

            <ULink
              as="button"
              to="#"
              variant="solid"
              size="md"
              class="relative rounded-full px-4 py-3 font-bold text-staco-dark hover:text-white bg-staco-green overflow-hidden group"
            >
              <span
                class="absolute inset-0 bg-staco-accent translate-y-full group-hover:translate-y-0 transition-transform duration-300 ease-out"
              ></span>
              <span
                class="relative z-10 inline-block group-hover:-translate-y-0.5 transition-transform duration-300 ease-out"
                >Start free</span
              >
            </ULink>
          </div>

          <div class="lg:hidden">
            <UButton
              class="p-1!"
              variant="ghost"
              :class="isScrolled ? 'text-gray-700' : 'text-black'"
              @click="isMobileMenuOpen = !isMobileMenuOpen"
            >
              <UIcon
                name="i-heroicons-bars-3-center-left"
                class="w-7 h-7 rotate-180"
              />
            </UButton>
          </div>
        </div>
      </div>
    </UContainer>

    <USlideover
      v-model:open="isMobileMenuOpen"
      side="left"
      :ui="{ header: 'border-0', body: 'p-4' }"
    >
      <template #header>
        <div class="w-full flex items-center justify-between">
          <img src="/logo-dark-2.svg" alt="Logo" class="h-10" />
          <UButton
            variant="ghost"
            color="neutral"
            @click="isMobileMenuOpen = false"
            class="p-0"
          >
            <UIcon name="i-heroicons-x-mark-20-solid" class="w-8 h-8" />
          </UButton>
        </div>
      </template>

      <template #body>
        <div class="flex flex-col h-full bg-white">
          <nav class="flex flex-col space-y-2">
            <NuxtLink
              v-for="link in links"
              :key="link.label"
              :to="link.to"
              class="py-4 text-sm font-medium border-b border-gray-300 text-gray-600 hover:bg-green-50 hover:text-green-600 transition flex justify-between group"
              @click="isMobileMenuOpen = false"
            >
              {{ link.label }}
            </NuxtLink>
          </nav>
        </div>
      </template>
    </USlideover>
  </header>
</template>

<script lang="ts" setup>
import { useWindowScroll } from "@vueuse/core";

// Scroll-based navbar visibility
const { y } = useWindowScroll();
const lastY = ref(0);
const isNavbarVisible = ref(true);
const isScrolled = ref(false);

const route = useRoute();

const isMobileMenuOpen = ref(false);
const activeTab = ref(0);
const indicatorLeft = ref(0);
const indicatorWidth = ref(0);
const tabRefs = ref<HTMLElement[]>([]);

const links = [
  { label: "Home", to: "/" },
  { label: "Pages", to: "#pages" }, // Kept as direct link
  { label: "Services", to: "#services" },
  { label: "Blogs", to: "#blog" },
  { label: "Contact Us", to: "#contact" },
];

const setTabRef = (
  el: Element | ComponentPublicInstance | null,
  index: number,
) => {
  if (el) {
    // If it's a component, get $el, otherwise it's the element itself
    tabRefs.value[index] =
      "$el" in el ? (el.$el as HTMLElement) : (el as HTMLElement);
  }
};

const setActiveTab = (index: number) => {
  activeTab.value = index;
  updateIndicator();
};

const updateIndicator = () => {
  const activeElement = tabRefs.value[activeTab.value];
  if (activeElement) {
    indicatorLeft.value = activeElement.offsetLeft;
    indicatorWidth.value = activeElement.offsetWidth;
  }
};

watch(y, (newY) => {
  isScrolled.value = newY > 50;

  if (newY <= 0) {
    isNavbarVisible.value = true;
    return;
  }

  const direction = newY > lastY.value ? "down" : "up";

  if (direction === "down" && newY > 100) {
    isNavbarVisible.value = false;
  } else {
    isNavbarVisible.value = true;
  }

  lastY.value = newY;
});

watch(
  () => route.path,
  () => {
    const index = links.findIndex((item) => item.to === route.path);
    if (index !== -1) {
      activeTab.value = index;
      nextTick(() => {
        updateIndicator();
      });
    }
  },
);

onMounted(() => {
  nextTick(() => updateIndicator());
  window.addEventListener("resize", updateIndicator);
});

onUnmounted(() => {
  window.removeEventListener("resize", updateIndicator);
});
</script>
