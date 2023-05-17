<template>
        <div class="flex flex-nowrap snap-x snap-mandatory overflow-x-auto scrollbar-hide" ref="showcase">

          <div
            class="mb-4 w-full lg:w-1/3 pr-4 shrink-0 snap-center"
            v-for="i in 10"
            :key="i"
          >
            <div class="p-5 bg-white shadow rounded">
              <svg
                class="mb-6 text-blue-800 h-8"
                viewBox="0 0 32 28"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M10.2418 12.749C9.45369 12.522 8.66554 12.4069 7.89887 12.4069C6.71496 12.4069 5.72709 12.6775 4.96109 13.0088C5.69957 10.3053 7.47358 5.6405 11.0075 5.11517C11.3348 5.0665 11.603 4.82986 11.6923 4.51131L12.4646 1.74875C12.5298 1.51512 12.4912 1.26505 12.3579 1.06231C12.2246 0.859563 12.0105 0.724288 11.7705 0.691393C11.5097 0.655812 11.2438 0.637686 10.9803 0.637686C6.73846 0.637686 2.53756 5.06516 0.764895 11.4046C-0.275679 15.1238 -0.580802 20.7154 1.98237 24.2349C3.41668 26.2043 5.50924 27.2559 8.20198 27.361C8.21305 27.3613 8.2238 27.3616 8.23487 27.3616C11.5573 27.3616 14.5035 25.1241 15.3997 21.9208C15.9351 20.0058 15.6931 17.9975 14.7176 16.2644C13.7526 14.5508 12.1632 13.3018 10.2418 12.749Z"
                  fill="currentColor"
                ></path>
                <path
                  d="M31.0396 16.2648C30.0746 14.5508 28.4852 13.3018 26.5638 12.749C25.7757 12.522 24.9875 12.4069 24.2212 12.4069C23.0373 12.4069 22.0491 12.6775 21.2831 13.0088C22.0215 10.3053 23.7955 5.6405 27.3298 5.11517C27.6571 5.0665 27.9249 4.82986 28.0146 4.51131L28.7869 1.74875C28.8521 1.51512 28.8135 1.26505 28.6802 1.06231C28.5473 0.859563 28.3331 0.724288 28.0928 0.691393C27.8323 0.655812 27.5664 0.637686 27.3026 0.637686C23.0608 0.637686 18.8599 5.06516 17.0869 11.4046C16.0466 15.1238 15.7415 20.7154 18.305 24.2356C19.739 26.2046 21.8319 27.2566 24.5243 27.3613C24.5354 27.3616 24.5461 27.362 24.5575 27.362C27.8796 27.362 30.8261 25.1244 31.7224 21.9211C32.2571 20.0061 32.0147 17.9975 31.0396 16.2648Z"
                  fill="currentColor"
                ></path>
              </svg>
              <p class="text-gray-500 leading-loose mb-4">
                這堂課程是我們的經典課程，透過基礎節奏樂訓練，讓孩子們學習如何使用節奏樂器，並且學習如何組合節奏，讓孩子們在音樂中找到自己的興趣。
              </p>
              <h4 class="font-bold font-heading">陳大文</h4>
              <p class="text-gray-500">學員家長</p>
            </div>
          </div>
      <button
        class="
          absolute
          left-4
          top-1/2
          mr-3
          lg:mr-0
          order-last
          lg:order-first
          bg-white
          p-4
          rounded-full
          shadow-md
          text-blue-800
          hover:text-blue-900
          hover:bg-gray-50
          transition
          duration-200
        "
        @click="scrollLeft"
        :class="{ 'opacity-0': !scroll.canScrollLeft }"
      >
        <svg
          class="w-6 h-6"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M10 19l-7-7m0 0l7-7m-7 7h18"
          ></path>
        </svg>
      </button>
      <button
        @click="scrollRight"
        class="
          absolute
          right-4
          top-1/2
          order-last
          bg-white
          p-4
          rounded-full
          shadow-md
          text-blue-800
          hover:text-blue-900
          hover:bg-gray-50
          transition
          duration-200
        "
        :class="{ 'opacity-0': !scroll.canScrollRight }"
      >
        <svg
          class="w-6 h-6"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M14 5l7 7m0 0l-7 7m7-7H3"
          ></path>
        </svg>
      </button>
    </div>
</template>

<script setup>
const showcase = ref(null);

const scroll = reactive({
  canScrollLeft: false,
  canScrollRight: true,
});

const scrollLeft = () => {
  nextTick(() => {
    showcase.value.scroll({
      left: showcase.value.scrollLeft - showcase.value.clientWidth / 3,
      behavior: "smooth",
    })
  });
};

const scrollRight = () => {
  nextTick(() => {
    showcase.value.scroll({
      left: showcase.value.scrollLeft + showcase.value.clientWidth / 3,
      behavior: "smooth",
    })
  });
};

onMounted(() => {
  showcase.value.addEventListener("scroll", (e) => {
    scroll.canScrollLeft = e.target.scrollLeft > 0;
    scroll.canScrollRight =
      e.target.scrollLeft + e.target.clientWidth < e.target.scrollWidth;
  });

  window.addEventListener('resize', () => {
    showcase.value.scroll({
      left: 0,
      behavior: "smooth",
    })
  });

});
</script>