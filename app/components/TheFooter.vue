<template>
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
                Staco is the dedicated platform for performance management that
                helps to grow your startup quickly
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
</template>

<script lang="ts" setup>
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
</script>
