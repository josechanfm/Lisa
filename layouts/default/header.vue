<template>
  <div class="sticky top-0 w-full z-40" id="nav-wrapper">
    <nav
      id="nav"
      :class="{ 'nav-shrink': shrink, 'with-sub-menu-open': showSubmenu }"
      class="relative bg-orange-500 transition-all overflow-clip"
      ref="nav"
    >
      <div
        class="max-w-7xl mx-auto flex justify-between items-center relative px-4"
        :class="shrink ? 'py-2 h-16' : 'py-6'"
      >
        <div class="lg:hidden order-last">
          <button class="navbar-burger p-3 text-white" @click="toggle">
            <svg
              class="block h-4 w-4 fill-current"
              viewBox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
            >
              <title>Mobile menu</title>
              <path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"></path>
            </svg>
          </button>
        </div>
        <NuxtLink :to="'/'">
          <div class="hidden lg:block text-sm text-white">主頁</div>
        </NuxtLink>
        <a class="" href="#">
          <div
            class="rounded-full hidden lg:block w-full md:w-auto mb-8 md:mb-0 py-3 px-8 text-center text-sm font-bold uppercase bg-gray-200 hover:bg-gray-100 transition duration-200"
          >
            聯絡我
          </div>
        </a>
      </div>
    </nav>

    <div
      class="w-full absolute transition-all overflow-hidden"
      :class="
        (showSubmenu ? 'shadow border-b h-screen md:h-auto' : 'h-0') +
        ' ' +
        (shrink ? 'bg-white' : 'bg-gray-50')
      "
      @mouseleave="leave"
    >
      <div
        class="overflow-auto h-full bg-orange-500"
        :class="shrink ? 'py-12' : 'py-12 pt-6'"
      >
        <div class="w-full">
          <ul class="w-full lg:hidden" v-if="!openedMenu">
            <li
              class="px-4 py-2 text-white hover:text-gray-800 text-lg"
              v-for="menuItem in menu"
            >
              <span v-if="menuItem.subMenu" @click="setHover(menuItem.subMenu)">{{
                menuItem.name
              }}</span>
              <NuxtLink class="" :to="menuItem?.link" v-else @click="toggle">{{
                menuItem.name
              }}</NuxtLink>
            </li>
          </ul>
        </div>
        <div class="max-w-7xl mx-auto px-4 grid md:grid-cols-3 gap-8">
          <div
            class="flex flex-col gap-3 text-lg font-medium capitalize justify-center py-2 text-white lg:hidden md:col-span-3"
            v-if="openedMenu"
          >
            <button @click="clearSel">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-6 h-6"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M10.5 19.5L3 12m0 0l7.5-7.5M3 12h18"
                />
              </svg>
            </button>
          </div>
          <div
            v-for="group in subMenu[openedMenu]?.items ?? []"
            :key="group.name"
            class=""
          >
            <h3 class="text-blue-800 font-semibold mb-4 text-sm">
              {{ group.name }}
            </h3>
            <ul class="text-gray-600 text-lg leading-10">
              <li
                v-for="item in group.children"
                :key="item.name"
                class="h-10 transition-all duration-50 hover:text-gray-800 hover:text-2xl hover:font-medium"
              >
                <NuxtLink :to="item.link" @click="toggle">
                  {{ item.name }}
                </NuxtLink>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import pkg from "lodash";

const { throttle } = pkg;

const shrink = ref(false);
const nav = ref(null);

const showSubmenu = ref(false);
const openedMenu = ref("");

const onScrollListener = throttle(() => {
  const navHeight = nav.value.offsetHeight;

  if (window.scrollY > navHeight && shrink.value === true) {
    return;
  }

  if (window.scrollY > navHeight) {
    shrink.value = true;
  } else {
    shrink.value = false;
  }
}, 10);

const setHover = (menu) => {
  showSubmenu.value = true;
  openedMenu.value = menu;

  document.body.style.overflow = "hidden";
};

const clearSel = () => {
  openedMenu.value = "";
};

const setLeave = () => {
  showSubmenu.value = false;
  clearSel();
};

const leave = () => {
  setLeave();
  document.body.style.overflow = "auto";
  openedMenu.value = "";
};

const toggle = () => {
  showSubmenu.value = !showSubmenu.value;

  if (showSubmenu.value) {
    document.body.style.overflow = "hidden";
  } else {
    leave();
  }
};

onMounted(() => {
  window.addEventListener("scroll", onScrollListener);
});

const menu = [
  {
    name: "主頁",
    link: "/",
  },
];

const subMenu = {
  courses: {
    name: "課程",
    items: [
      {
        name: "課程",
        children: [
          {
            name: "查看全部課程",
            link: "/courses",
          },
        ],
      },
      {
        name: "音樂課程",
        children: [
          {
            name: "幼兒啓蒙音樂課程",
            link: "/courses/1",
          },
          {
            name: "兒童音樂系統課程",
            link: "/courses/2",
          },
          {
            name: "青少年音樂課程",
            link: "/courses/3",
          },
          {
            name: "成人合唱專業訓練班",
            link: "/courses/4",
          },
        ],
      },
      {
        name: "其他課程",
        children: [
          {
            name: "奧數",
            link: "#",
          },
          {
            name: "英語主持",
            link: "#",
          },
          {
            name: "幼兒體操啓蒙班",
            link: "#",
          },
          {
            name: "禮儀",
            link: "#",
          },
          {
            name: "閱讀思維",
            link: "#",
          },
          {
            name: "美術",
            link: "#",
          },
        ],
      },
    ],
  },
};
</script>
