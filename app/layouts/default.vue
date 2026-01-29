<template>
  <UApp>
    <header
      class="absolute top-0 z-50 w-full bg-white lg:bg-transparent backdrop-blur-sm lg:py-4"
    >
      <UContainer>
        <div
          class="relative flex items-center justify-between h-20 lg:rounded-full"
        >
          <div
            class="absolute hidden inset-0 rounded-full bg-linear-to-b from-neutral-700 to-neutral-800 shadow-[0_8px_32px_rgba(0,0,0,0.6),0_2px_8px_rgba(0,0,0,0.4),inset_0_1px_0_rgba(255,255,255,0.1),inset_0_-1px_2px_rgba(0,0,0,0.5)] lg:block"
          ></div>
          <div
            class="absolute hidden inset-0.75 rounded-full bg-linear-to-b from-neutral-800 to-neutral-900 shadow-[inset_0_2px_4px_rgba(0,0,0,0.8),inset_0_-1px_2px_rgba(255,255,255,0.05) lg:block]"
          ></div>

          <div
            class="w-full flex items-center justify-between h-20 lg:px-4 lg:py- lg:absolute lg:rounded-full"
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
              >
                {{ link.label }}
              </NuxtLink>
            </nav>

            <div class="hidden lg:flex items-center gap-4">
              <ULink
                to="#"
                class="text-sm font-semibold text-white hover:text-green-600"
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
                class="text-gray-600 p-1!"
                variant="ghost"
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

    <UMain>
      <slot />
    </UMain>

    <div class="mt-20 bg-staco-light pt-20 pb-5">
      <footer class="bg-staco-dark text-white mx-5 rounded-[30px]">
        <UContainer>
          <div class="py-16 lg:py-20">
            <div class="grid lg:grid-cols-6 gap-2 lg:gap-12">
              <!-- Brand Column -->
              <div class="space-y-6 lg:col-span-2">
                <ULink to="/" class="inline-block">
                  <img src="/logo-light.svg" alt="Staco Logo" />
                </ULink>

                <p class="text-staco-light text-sm leading-relaxed max-w-xs">
                  Staco is the dedicated platform for performance management
                  that helps to grow your startup quickly
                </p>

                <!-- Social Links -->
                <div
                  class="flex items-center justify-center gap-4 pt-2 md:justify-start"
                >
                  <ULink
                    v-for="social in socialLinks"
                    :key="social.icon"
                    variant="ghost"
                    size="md"
                    class="rounded-full p-3 flex items-center justify-center border-2 border-white/15 hover:bg-white/10 hover:text-white transition-all duration-300"
                  >
                    <UIcon :name="social.icon" class="w-4 h-4" />
                  </ULink>
                </div>
              </div>

              <div
                class="grid grid-cols-2 md:grid-cols-4 gap-8 md:gap-4 lg:gap-8 lg:col-span-4"
              >
                <!-- Products -->
                <div class="space-y-5">
                  <h6
                    class="font-bold text-white text-base flex items-center gap-2 uppercase"
                  >
                    Products <span class="text-lg">🔥</span>
                  </h6>
                  <ul class="space-y-3">
                    <li v-for="item in footerLinks.products" :key="item">
                      <ULink
                        to="#"
                        class="text-gray-400 hover:text-white transition-colors text-sm inline-flex items-center"
                        :ui="{ base: 'hover:no-underline' }"
                      >
                        <span>{{ item }}</span>
                      </ULink>
                    </li>
                  </ul>
                </div>

                <!-- Why Choose -->
                <div class="space-y-5">
                  <h6
                    class="font-bold text-white text-base flex items-center gap-2 uppercase"
                  >
                    Why choose <span class="text-lg">🌟</span>
                  </h6>
                  <ul class="space-y-3">
                    <li v-for="item in footerLinks.whyChoose" :key="item">
                      <ULink
                        to="#"
                        class="text-gray-400 hover:text-white transition-colors text-sm inline-flex items-center"
                        :ui="{ base: 'hover:no-underline' }"
                      >
                        <span>{{ item }}</span>
                      </ULink>
                    </li>
                  </ul>
                </div>

                <!-- Resources -->
                <div class="space-y-5">
                  <h6
                    class="font-bold text-white text-base flex items-center gap-2 uppercase"
                  >
                    Resources <span class="text-lg">❇️</span>
                  </h6>
                  <ul class="space-y-3">
                    <li v-for="item in footerLinks.resources" :key="item">
                      <ULink
                        to="#"
                        class="text-gray-400 hover:text-white transition-colors text-sm inline-flex items-center"
                        :ui="{ base: 'hover:no-underline' }"
                      >
                        <span>{{ item }}</span>
                      </ULink>
                    </li>
                  </ul>
                </div>

                <!-- Company -->
                <div class="space-y-5">
                  <h6
                    class="font-bold text-white text-base flex items-center gap-2 uppercase"
                  >
                    Company <span class="text-lg">💎</span>
                  </h6>
                  <ul class="space-y-3">
                    <li v-for="item in footerLinks.company" :key="item">
                      <ULink
                        to="#"
                        class="text-gray-400 hover:text-white transition-colors text-sm inline-flex items-center"
                        :ui="{ base: 'hover:no-underline' }"
                      >
                        <span>{{ item }}</span>
                      </ULink>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </UContainer>

        <!-- Footer Bottom -->
        <!-- <UDivider class="opacity-20" /> -->
        <UContainer>
          <div class="py-6 lg:py-8">
            <div
              class="flex flex-col md:flex-row justify-between items-center gap-4"
            >
              <div
                class="w-full flex flex-wrap justify-center gap-6 md:justify-between"
              >
                <div class="flex items-center gap-4 md:order-2">
                  <ULink
                    v-for="link in privacyLinks"
                    :key="link.label"
                    :to="link.to"
                    class="text-gray-400 hover:text-white transition-colors text-sm"
                    :ui="{ base: 'hover:no-underline' }"
                  >
                    {{ link.label }}
                  </ULink>
                </div>

                <p class="text-gray-400 text-sm md:order-1">
                  © {{ new Date().getFullYear() }}
                  <ULink
                    to="/"
                    class="font-semibold text-gray-400"
                    :ui="{ base: 'hover:no-underline' }"
                  >
                    Staco
                  </ULink>
                  . All rights reserved.
                </p>
              </div>
            </div>
          </div>
        </UContainer>
      </footer>
    </div>
  </UApp>
</template>

<script lang="ts" setup>
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

const socialLinks = [
  { icon: "i-simple-icons-facebook" },
  { icon: "i-simple-icons-x" },
  { icon: "i-simple-icons-linkedin" },
  { icon: "i-simple-icons-instagram" },
  { icon: "i-simple-icons-youtube" },
];

const footerLinks = {
  products: [
    "HR Management",
    "Invoice System",
    "Email Marketing",
    "Web Services",
    "Digital Marketing",
  ],
  whyChoose: ["Customers", "Why Staco ?", "Book a demo"],
  resources: ["Latest Blog", "Supports", "Knowledgebase", "FAQs"],
  company: ["About", "What we do", "Contact us", "Careers"],
};

const privacyLinks = [
  { label: "Terms and conditions", to: "#" },
  { label: "Cookies", to: "#" },
  { label: "Privacy policy", to: "#" },
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
