<template>
  <UPageSection
    class="mt-20 bg-white xl:mt-35"
    :ui="{ container: 'py-0! sm:py-0!' }"
  >
    <div class="grid gap-7.5 sm:grid-cols-2 lg:grid-cols-3">
      <UCard
        v-for="(feature, index) in features"
        :key="index"
        variant="soft"
        class="bg-staco-light py-10 px-7.5 rounded-[30px] group transition duration-300"
        :ui="{ body: 'p-0 sm:p-0' }"
        v-motion-slide-visible-once-bottom
        :delay="index * 50"
      >
        <div class="w-12.5 h-12.5 flex items-center justify-center mb-8">
          <img :src="feature.iconSvg" alt="icon" />
        </div>

        <h3 class="text-lg font-bold mb-5">
          {{ feature.title }}
        </h3>

        <p class="mb-10 md:mb-17">
          {{ feature.description }}
        </p>

        <UButton
          variant="link"
          class="w-full text-staco-dark p-0 group-hover:text-staco-accent flex items-center justify-between"
        >
          <span class="font-bold">Learn more</span>
          <div
            class="h-10 w-10 rounded-full bg-black/10 group-hover:-rotate-45 group-hover:bg-staco-accent group-hover:text-white transition-transform duration-300 ease-out flex items-center justify-center"
          >
            <UIcon name="i-lucide-arrow-right" class="w-6 h-6" />
          </div>
        </UButton>
      </UCard>
    </div>
  </UPageSection>
</template>

<script lang="ts" setup>
const features = [
  {
    iconSvg:
      "data:image/svg+xml,%3csvg width='50' height='50' viewBox='0 0 50 50' fill='none' xmlns='http://www.w3.org/2000/svg'%3e%3cpath d='M38.75 39.5752H34.125C33.1 39.5752 32.25 38.7252 32.25 37.7002C32.25 36.6752 33.1 35.8252 34.125 35.8252H38.75C39.775 35.8252 40.625 36.6752 40.625 37.7002C40.625 38.7252 39.775 39.5752 38.75 39.5752Z' fill='%23004D42'/%3e%3cpath d='M27.425 39.5752H11.25C10.225 39.5752 9.375 38.7252 9.375 37.7002C9.375 36.6752 10.225 35.8252 11.25 35.8252H27.425C28.45 35.8252 29.3 36.6752 29.3 37.7002C29.3 38.7252 28.475 39.5752 27.425 39.5752Z' fill='%23004D42'/%3e%3cpath d='M38.7508 30.175H24.9258C23.9008 30.175 23.0508 29.325 23.0508 28.3C23.0508 27.275 23.9008 26.425 24.9258 26.425H38.7508C39.7758 26.425 40.6258 27.275 40.6258 28.3C40.6258 29.325 39.7758 30.175 38.7508 30.175Z' fill='%23004D42'/%3e%3cpath d='M18.175 30.175H11.25C10.225 30.175 9.375 29.325 9.375 28.3C9.375 27.275 10.225 26.425 11.25 26.425H18.175C19.2 26.425 20.05 27.275 20.05 28.3C20.05 29.325 19.2 30.175 18.175 30.175Z' fill='%23004D42'/%3e%3cpath opacity='0.4' d='M35.475 0H14.525C5.425 0 0 5.425 0 14.525V35.45C0 44.575 5.425 50 14.525 50H35.45C44.55 50 49.975 44.575 49.975 35.475V14.525C50 5.425 44.575 0 35.475 0Z' fill='%23004D42'/%3e%3c/svg%3e",
    title: "Used advanced technologies",
    description:
      "I must explain to you how all this mistaken. Idea of main denouncing pleasure and praising pain was born",
  },
  {
    iconSvg:
      "data:image/svg+xml,%3csvg width='50' height='50' viewBox='0 0 50 50' fill='none' xmlns='http://www.w3.org/2000/svg'%3e%3cpath opacity='0.4' d='M50 25C50 37.6 40.6499 48.025 28.5249 49.75C27.3749 49.925 26.2 50 25 50C18.1 50 11.85 47.2 7.32498 42.675C2.79998 38.15 0 31.9 0 25C0 11.2 11.2 0 25 0C31.9 0 38.15 2.8 42.675 7.325C47.2 11.85 50 18.1 50 25Z' fill='%2344C486'/%3e%3cpath d='M32.0759 20.5748L25.8758 26.7748L42.2008 43.0998C41.3008 43.9748 40.3258 44.7748 39.3008 45.4998L23.2258 29.4248L17.0508 35.5998L29.8508 48.4248C30.1258 48.6998 30.3009 49.0498 30.3759 49.3998C30.3759 49.3998 30.3759 49.3998 30.3759 49.4248C29.7759 49.5498 29.1508 49.6748 28.5258 49.7498C27.7258 49.8748 26.9258 49.9498 26.1008 49.9748L14.4008 38.2498L8.70078 43.9498C8.22578 43.5498 7.77581 43.1248 7.32581 42.6748C6.87581 42.2248 6.45078 41.7748 6.05078 41.2998L41.3009 6.0498C41.7759 6.4498 42.2258 6.8748 42.6758 7.3248C43.1258 7.7748 43.5509 8.2248 43.9509 8.6998L34.7259 17.9248L48.9509 32.1498C48.5509 33.4748 48.0508 34.7248 47.4508 35.9498L32.0759 20.5748Z' fill='%2344C486'/%3e%3c/svg%3e",
    title: "Clean design & Typography",
    description:
      "I must explain to you how all this mistaken. Idea of main denouncing pleasure and praising pain was born",
  },
  {
    iconSvg:
      "data:image/svg+xml,%3csvg width='50' height='50' viewBox='0 0 50 50' fill='none' xmlns='http://www.w3.org/2000/svg'%3e%3cpath opacity='0.4' d='M50 12.5V37.5C50 45 45.8333 50 36.1111 50H13.8889C4.16667 50 0 45 0 37.5V12.5C0 5 4.16667 0 13.8889 0H36.1111C45.8333 0 50 5 50 12.5Z' fill='%23433968'/%3e%3cpath d='M34.7218 0V18.7909C34.7218 19.8428 33.2773 20.3688 32.3884 19.6755L25.9441 14.5594C25.4163 14.129 24.5828 14.129 24.055 14.5594L17.6108 19.6755C16.7219 20.3927 15.2773 19.8428 15.2773 18.7909V0H34.7218Z' fill='%23433968'/%3e%3cpath d='M40.2795 30.875H28.474C27.3351 30.875 26.3906 30.025 26.3906 29C26.3906 27.975 27.3351 27.125 28.474 27.125H40.2795C41.4184 27.125 42.3628 27.975 42.3628 29C42.3628 30.025 41.4184 30.875 40.2795 30.875Z' fill='%23433968'/%3e%3cpath d='M40.2765 40.875H16.6654C15.5265 40.875 14.582 40.025 14.582 39C14.582 37.975 15.5265 37.125 16.6654 37.125H40.2765C41.4154 37.125 42.3598 37.975 42.3598 39C42.3598 40.025 41.4154 40.875 40.2765 40.875Z' fill='%23433968'/%3e%3c/svg%3e",
    title: "Best customer support",
    description:
      "I must explain to you how all this mistaken. Idea of main denouncing pleasure and praising pain was born",
  },
];
</script>
