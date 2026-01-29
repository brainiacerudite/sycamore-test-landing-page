<template>
  <div>
    <UPageSection class="relative bg-staco-card overflow-hidden lg:pb-4">
      <span
        v-for="(icon, index) in backgroundIcons"
        :key="index"
        class="absolute z-0 pointer-events-none"
        :class="icon.positionClass"
        v-html="icon.svg"
      />

      <UContainer
        class="px-0! pt-26 pb-10 md:pt-16 md:pb-2 lg:pb-0 lg:px-4 xl:pt-32 xl:pb-18"
      >
        <span
          class="hidden md:block absolute h-[34%] right-[18%] -top-16 z-20 scale-80 lg:h-[44%] lg:right-[26.5%] lg:-top-10 xl:scale-100 xl:right-[25%] opacity-60"
        >
          <svg
            width="299"
            height="353"
            viewBox="0 0 299 353"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M82.8994 299.957C1.6656 202.325 -35.6931 344.357 74.3868 347.838C184.467 351.319 385.434 265.915 246.722 0.984375"
              stroke="#B2EDA1"
              stroke-width="10"
              stroke-miterlimit="10"
            />
          </svg>
        </span>
        <span
          class="hidden md:block absolute h-[59%] right-[29%] bottom-30 z-0 scale-80 lg:h-[69%] lg:right-[35%] lg:bottom-18 xl:scale-100 xl:right-[32%] xl:-bottom-2 opacity-60"
        >
          <svg
            width="275"
            height="605"
            viewBox="0 0 275 605"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M1.71289 599.989C1.71289 599.989 468.069 436.813 169.913 2.97119"
              stroke="#B2EDA1"
              stroke-width="10"
              stroke-miterlimit="10"
            />
          </svg>
        </span>

        <div class="flex flex-col gap-12 md:gap-6 md:flex-row lg:items-start">
          <!-- Left Content -->
          <div
            class="md:w-1/2 md:flex-[0_0_auto] space-y-8 text-white"
            v-motion
            :initial="{ opacity: 0, y: 100 }"
            :enter="{
              opacity: 1,
              y: 0,
              transition: { duration: 800, ease: 'easeOut' },
            }"
          >
            <h1
              class="text-[34px] md:text-[40px] lg:text-6xl font-bold leading-tight"
            >
              Financial Security Made
              <span
                class="text-staco-green mt-2 relative inline-block -translate-y-1"
              >
                <span ref="rotatingText" class="inline-block mb-1">Easier</span>
                <span
                  class="absolute bottom-0 left-0 h-2 bg-staco-green transition-all ease-linear"
                  :class="isAnimating ? 'duration-2900' : 'duration-0'"
                  :style="{ width: progressWidth + '%' }"
                />
              </span>
            </h1>

            <p class="text-lg text-white max-w-xl leading-9">
              Staco is the dedicated platform for human management that helps to
              grow your startup business quickly
            </p>

            <div class="flex flex-wrap gap-8 items-center pt-4">
              <AppLinkButton to="#" size="xl">
                Get Start For Free
              </AppLinkButton>

              <ULink
                as="button"
                to="#"
                size="xl"
                variant="ghost"
                class="text-white flex items-center gap-2 hover:bg-transparent hover:text-staco-accent group"
              >
                <span>Let's talk</span>
                <span
                  class="w-7.5 h-7.5 flex items-center justify-center rounded-full bg-white/10 group-hover:bg-staco-accent"
                >
                  <UIcon
                    name="i-lucide-chevron-right"
                    class="w-4 h-4 group-hover:text-white group-hover:-rotate-45 transition-transform duration-300 ease-out"
                  />
                </span>
              </ULink>
            </div>
          </div>

          <!-- Right Content - Video -->
          <div
            class="md:w-1/2 md:flex-[0_0_auto] md:pr-4"
            v-motion
            :initial="{ opacity: 0, x: 100 }"
            :enter="{
              opacity: 1,
              x: 0,
              transition: { duration: 1000, delay: 200, ease: 'easeOut' },
            }"
          >
            <div>
              <div
                class="relative z-10 flex items-center justify-center max-w-117.5 w-full mr-auto h-full lg:mr-4 lg:ml-auto"
              >
                <div
                  class="rounded-[30px] overflow-hidden relative h-85 after:absolute after:inset-0 after:bg-linear-to-br after:from-transparent after:via-transparent after:to-black/80 after:z-1"
                >
                  <video
                    ref="videoElement"
                    class="w-full h-full object-cover"
                    loop
                    muted
                    autoplay
                    playsinline
                  >
                    <source src="/h6-video-DaLtBHE1.mp4" type="video/mp4" />
                    Your browser does not support the video tag.
                  </video>
                  <UButton
                    variant="solid"
                    size="lg"
                    class="absolute z-10 bottom-6 right-6 bg-white text-staco-accent rounded-full w-12 h-12 p-0 flex items-center justify-center hover:text-white"
                    @click="togglePlayback"
                  >
                    <UIcon
                      :name="
                        isPlaying
                          ? 'i-heroicons-pause-20-solid'
                          : 'i-heroicons-play-20-solid'
                      "
                      class="w-5 h-5 text-navy-900"
                    />
                  </UButton>
                </div>
              </div>
            </div>
          </div>
        </div>
      </UContainer>
    </UPageSection>

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
          v-motion-slide-visible-bottom
          :delay="index * 200"
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

    <UPageSection class="mt-10 bg-white">
      <UCard
        class="bg-staco-teal overflow-hidden rounded-[30px]"
        :ui="{ body: 'p-0' }"
        v-motion-fade-visible
        :duration="800"
      >
        <div
          class="grid md:grid-cols-2 gap-2 items-center px-12 lg:px-16 xl:px-17.5"
        >
          <!-- Left Content -->
          <div
            class="space-y-8.5 py-12 text-center md:text-left lg:py-16 xl:pt-13.5 xl:pb-17.5"
          >
            <h2
              class="text-[36px] md:text-[38px] lg:text-5xl font-bold text-white leading-tight"
            >
              We are building <br />financial foundations
            </h2>

            <UButton
              size="xl"
              class="rounded-full px-5 py-3 bg-staco-green text-staco-dark hover:bg-staco-green-dark font-semibold"
              trailing-icon="i-lucide-arrow-right"
            >
              Let's Talk
            </UButton>
          </div>

          <!-- Right Content - Illustration -->
          <div
            class="relative h-64 lg:h-80 flex items-end justify-center"
            v-motion-slide-visible-right
            :delay="300"
          >
            <img
              src="data:image/svg+xml,%3csvg%20width='372'%20height='250'%20viewBox='0%200%20372%20250'%20fill='none'%20xmlns='http://www.w3.org/2000/svg'%3e%3cpath%20d='M120.81%20137.65L15.7733%20235.304L0%20249.943L46.5404%20250L58.3819%20235.35L137.134%20137.65H120.81Z'%20fill='%2395A196'/%3e%3cpath%20d='M149.295%20137.65L90.2023%20235.304L81.3184%20249.943L127.882%20250L132.822%20235.35L165.618%20137.65H149.295Z'%20fill='%2385A088'/%3e%3cpath%20d='M177.781%20137.65L164.622%20235.304L162.627%20249.943L209.225%20250L207.276%20235.35L194.105%20137.65H177.781Z'%20fill='%235C9F63'/%3e%3cpath%20d='M206.268%20137.65L239.052%20235.304L243.947%20249.943L290.579%20250L281.73%20235.35L222.591%20137.65H206.268Z'%20fill='%23439F4D'/%3e%3cpath%20d='M234.754%20137.65L313.471%20235.304L325.267%20249.943L371.922%20250L356.172%20235.35L251.077%20137.65H234.754Z'%20fill='%23019D12'/%3e%3cpath%20d='M137.134%20105.312H120.811V137.65H137.134V105.312Z'%20fill='%2322675D'/%3e%3cpath%20d='M165.62%2086.6959H149.297V137.65H165.62V86.6959Z'%20fill='%2330766C'/%3e%3cpath%20d='M194.105%2066.1309H177.781V137.65H194.105V66.1309Z'%20fill='%233A8A7F'/%3e%3cpath%20d='M222.591%2045.1879H206.268V137.65H222.591V45.1879Z'%20fill='%236CA88B'/%3e%3cpath%20d='M251.077%2023.8549H234.754V137.65H251.077V23.8549Z'%20fill='%2344C486'/%3e%3cpath%20d='M120.81%20137.65L15.7733%20235.304L0%20249.943L46.5404%20250L58.3819%20235.35L137.134%20137.65H120.81Z'%20fill='white'/%3e%3cpath%20d='M149.295%20137.65L90.2023%20235.304L81.3184%20249.943L127.882%20250L132.822%20235.35L165.618%20137.65H149.295Z'%20fill='white'/%3e%3cpath%20d='M177.781%20137.65L164.622%20235.304L162.627%20249.943L209.225%20250L207.276%20235.35L194.105%20137.65H177.781Z'%20fill='white'/%3e%3cpath%20d='M206.268%20137.65L239.052%20235.304L243.947%20249.943L290.579%20250L281.73%20235.35L222.591%20137.65H206.268Z'%20fill='white'/%3e%3cpath%20d='M234.754%20137.65L313.471%20235.304L325.267%20249.943L371.922%20250L356.172%20235.35L251.077%20137.65H234.754Z'%20fill='white'/%3e%3cpath%20d='M127.919%2087.8536L108.764%20114.609H147.085L127.919%2087.8536Z'%20fill='%2322675D'/%3e%3cpath%20d='M157.596%2065.168L138.43%2091.9115H176.751L157.596%2065.168Z'%20fill='%2330766C'/%3e%3cpath%20d='M185.52%2043.0557L166.365%2069.7992H204.687L185.52%2043.0557Z'%20fill='%233A8A7F'/%3e%3cpath%20d='M214.419%2022.1124L195.264%2048.856H233.585L214.419%2022.1124Z'%20fill='%236CA88B'/%3e%3cpath%20d='M242.536%200L223.381%2026.7435H261.702L242.536%200Z'%20fill='%2344C486'/%3e%3c/svg%3e"
              alt="img"
            />
          </div>
        </div>
      </UCard>
    </UPageSection>

    <UPageSection
      class="mt-10 bg-white border-y border-black/15"
      :ui="{ container: 'py-0! relative xl:px-0!' }"
    >
      <div
        class="absolute inset-0 flex items-center justify-center pointer-events-none overflow-hidden opacity-30"
        v-motion
        :initial="{ y: 50, opacity: 0 }"
        :visible="{ y: 0, opacity: 0.3, transition: { duration: 1500 } }"
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
  </div>
</template>

<script lang="ts" setup>
import { useElementVisibility, useTransition } from "@vueuse/core";

const rotatingText = ref<HTMLElement | null>(null);
const videoElement = ref<HTMLVideoElement | null>(null);
const counterSection = ref<HTMLElement | null>(null);
const isPlaying = ref(true);
const progressWidth = ref(0);
const isAnimating = ref(false);

let currentIndex = 0;
const words = ["Easier", "Accountable", "Unbeatable"];

const statsData = [
  { target: 200, suffix: "", label: "Countries Worldwide" },
  { target: 156, suffix: "K", label: "Registered User" },
  { target: 23, suffix: "K", label: "Small & Big Companies" },
];

const backgroundIcons = [
  {
    positionClass: "right-[20%] top-[20%]",
    svg: `<img src="data:image/svg+xml,%3csvg width='39' height='45' viewBox='0 0 39 45' fill='none' xmlns='http://www.w3.org/2000/svg'%3e%3cpath d='M4.35993 8.12197C-0.593748 13.8731 -1.08911 28.1803 2.52242 35.9656C7.8417 47.1326 27.7987 47.1679 33.3327 36.604C37.5794 28.3821 36.4727 17.5359 38.6821 0.572389C22.3362 3.68367 9.16665 2.37763 4.35993 8.12197Z' fill='%23B2EDA1' fill-opacity='0.3'/%3e%3c/svg%3e" alt="bg-shape-1" />`,
  },
  {
    positionClass: "left-[44%] top-[35%]",
    svg: `<img src="data:image/svg+xml,%3csvg width='52' height='41' viewBox='0 0 52 41' fill='none' xmlns='http://www.w3.org/2000/svg'%3e%3cpath d='M18.6144 0.0465448C13.3054 -0.784969 1.64645 9.71291 0.397269 16.469C-1.99699 29.5653 6.64316 41.5183 20.5923 40.8947C28.816 40.4789 36.6234 31.2283 51.9258 21.2502C36.4152 10.7523 28.0873 1.81351 18.6144 0.0465448Z' fill='%23B2EDA1' fill-opacity='0.3'/%3e%3c/svg%3e" alt="bg-shape-2" />`,
  },
  {
    positionClass: "left-[35%] top-[18%]",
    svg: `<img src="data:image/svg+xml,%3csvg width='49' height='47' viewBox='0 0 49 47' fill='none' xmlns='http://www.w3.org/2000/svg'%3e%3cpath d='M8.82762 7.31652C-2.25929 15.2616 -1.57861 29.3022 8.24752 39.1752C17.8521 48.9776 31.6961 50.2641 39.7268 38.9026C45.4458 31.1026 44.49 18.684 48.0973 0.246201C29.4497 3.29007 16.6336 1.84265 8.82762 7.31652Z' fill='%23B2EDA1' fill-opacity='0.3'/%3e%3c/svg%3e" alt="bg-shape-3" />`,
  },
];

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

const animateProgress = () => {
  isAnimating.value = false;
  progressWidth.value = 0;
  setTimeout(() => {
    isAnimating.value = true;
    progressWidth.value = 100;
  }, 100);
  setTimeout(() => {
    currentIndex = (currentIndex + 1) % words.length;
    if (rotatingText.value)
      rotatingText.value.textContent = words[currentIndex] ?? "";
    animateProgress();
  }, 3000);
};

const togglePlayback = () => {
  if (videoElement.value) {
    isPlaying.value ? videoElement.value.pause() : videoElement.value.play();
    isPlaying.value = !isPlaying.value;
  }
};

// Watch visibility to trigger animation
watch(targetIsVisible, (isVisible) => {
  if (isVisible) {
    stats.forEach((stat) => {
      stat.source.value = stat.target;
    });
  }
});

onMounted(() => {
  animateProgress();
});
</script>
