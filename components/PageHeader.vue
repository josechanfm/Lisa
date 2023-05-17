<template>
  <section class="relative header" ref="header">
    <div class="bg-orange-500 text-white">
      <div class="max-w-7xl mx-auto p-4 pt-6 pb-12">
        <nav class="flex py-3 mb-4" aria-label="Breadcrumb" v-if="breadcrumbs">
          <ol class="inline-flex items-center space-x-1 md:space-x-3">
            <li class="inline-flex items-center">
              <NuxtLink to="/" class="text-sm inline-flex items-center">
                <svg
                  class="w-4 h-4 mr-2"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M10.707 2.293a1 1 0 00-1.414 0l-7 7a1 1 0 001.414 1.414L4 10.414V17a1 1 0 001 1h2a1 1 0 001-1v-2a1 1 0 011-1h2a1 1 0 011 1v2a1 1 0 001 1h2a1 1 0 001-1v-6.586l.293.293a1 1 0 001.414-1.414l-7-7z"
                  ></path>
                </svg>
                主頁
              </NuxtLink>
            </li>
            <li v-for="path in breadcrumbs" :key="path.to">
              <div class="flex items-center">
                <svg
                  class="w-6 h-6"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    fill-rule="evenodd"
                    d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
                    clip-rule="evenodd"
                  ></path>
                </svg>
                <NuxtLink
                  class="ml-1 md:ml-2 text-sm font-medium"
                  :to="path.to ?? null"
                  >{{ path.text }}</NuxtLink
                >
              </div>
            </li>
          </ol>
        </nav>
        <h1 class="font-medium leading-relaxed" :class="textSize">{{ title }}</h1>
        <h2 class="text-2xl" v-if="subtitle">{{ subtitle }}</h2>
      </div>
    </div>

    <div class="skew skew-bottom mr-for-radius">
      <svg
        class="h-8 md:h-12 lg:h-20 w-full text-gray-50"
        viewBox="0 0 10 10"
        preserveAspectRatio="none"
      >
        <polygon fill="currentColor" points="0 0 10 0 0 10"></polygon>
      </svg>
    </div>

    <div
      class="fixed left-0 right-0 bg-white backdrop-blur-lg -top-16 box-border"
      :class="
        (coverNav ? 'z-40' : 'z-30') + ' ' + (isFinalized ? 'border-b' : 'border-none')
      "
      ref="headerSecondary"
    >
      <div class="max-w-7xl mx-auto p-4 h-16 flex">
        <h1 class="text-xl font-semibold flex-1 truncate">{{ title }}</h1>
        <div>
          <slot name="extra"></slot>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const header = ref(null);
const headerSecondary = ref(null);

const nav = ref(null);

const translateY = ref(0);

const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  subtitle: {
    type: String,
    required: false,
  },
  coverNav: {
    type: Boolean,
    required: false,
    default: true,
  },
  breadcrumbs: {
    type: Array,
    required: false,
  },
});

const isFinalized = computed(() => {
  return !props.coverNav ? true : translateY.value === 64;
});
const textSize = computed(() => {
  if (props.title.length > 20) {
    return "text-2xl md:text-4xl";
  } else {
    return "text-5xl";
  }
});

const easing = (x) => {
  return x < 0.5 ? 16 * x * x * x * x * x : 1 - Math.pow(-2 * x + 2, 5) / 2;
};

const scrollListener = () => {
  const offsetNav = nav.value.offsetHeight;

  nav.value.style.height = nav.value.children[0].offsetHeight + "px";
  // get the header height
  const headerHeight = header.value.offsetHeight;
  // get the header secondary height
  const headerSecondaryHeight = headerSecondary.value.offsetHeight;

  // get the scroll position
  const scrollPosition = window.scrollY;

  const minOffset = 64 + (props.coverNav ? 0 : offsetNav);

  translateY.value = Math.min(
    minOffset,
    Math.max(0, scrollPosition - headerHeight + headerSecondaryHeight)
  );

  translateY.value = easing(translateY.value / minOffset) * minOffset;

  if (props.coverNav) {
    nav.value.children[0].style.transform = `translateY(${translateY.value}px)`;
    // disable nav click
    nav.value.children[0].style.pointerEvents = translateY.value === 0 ? "all" : "none";
  }

  headerSecondary.value.style.transform = `translateY(${translateY.value}px)`;
};

onMounted(() => {
  nav.value = document.getElementById("nav");
  window.addEventListener("scroll", scrollListener);
});

onUnmounted(() => {
  window.removeEventListener("scroll", scrollListener);
  nav.value.style.height = "auto";
});
</script>

<style scoped></style>
