<template>
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
        class="hidden md:block absolute h-[34%] right-[18%] -top-16 z-20 scale-80 lg:h-[44%] lg:right-[26.5%] lg:-top-10 xl:scale-100 xl:right-[25%]"
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
        class="hidden md:block absolute h-[59%] right-[29%] bottom-30 z-0 scale-80 lg:h-[69%] lg:right-[35%] lg:bottom-18 xl:scale-100 xl:right-[32%] xl:-bottom-2"
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
            transition: { duration: 500, ease: 'easeOut' },
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
            <AppLinkButton to="#" size="xl"> Get Start For Free </AppLinkButton>

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
          :initial="{ opacity: 0, y: 100 }"
          :enter="{
            opacity: 1,
            y: 0,
            transition: { duration: 600, delay: 200, ease: 'easeOut' },
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
</template>

<script lang="ts" setup>
const rotatingText = ref<HTMLElement | null>(null);
const videoElement = ref<HTMLVideoElement | null>(null);
const isPlaying = ref(true);
const progressWidth = ref(0);
const isAnimating = ref(false);

let currentIndex = 0;
const words = ["Easier", "Accountable", "Unbeatable"];

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

onMounted(() => {
  animateProgress();
});
</script>
