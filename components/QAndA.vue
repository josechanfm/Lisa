<template>
  <ul class="space-y-4 lg:space-y-6">
    <li class="p-6 bg-gray-50 rounded shadow" v-for="(question, i) in questions"
        :key="i"
    >
      <button
        @click="toggle(i)"
        class="
          w-full
          flex
          justify-between
          items-center
          text-left
          font-bold font-heading
          hover:text-gray-600
        "
      >
        <span class="text-xl">{{ question.question }}</span>
        <svg
          class="w-4 h-4 text-blue-600"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          v-if="isOpened(i)"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M5 10l7-7m0 0l7 7m-7-7v18"
          ></path>
        </svg>
        <svg
          class="w-4 h-4 text-blue-600"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          v-else
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M19 14l-7 7m0 0l-7-7m7 7V3"
          ></path>
        </svg>
      </button>
      <p class="text-gray-400 font-normal leading-loose transition-all duration-300 ease-in-out overflow-hidden"
          :class="isOpened(i) ? 'mt-4 h-auto' : 'h-0'"
      >
        本會導師均為專業幼兒音樂導師，擁有多年豐富幼兒音樂教學經驗及畢業於香港浸會大學、香港教育學院、持音樂學士(音樂教育)、幼兒音樂教育專業證書、
        合格幼稚園教師及PGDE 學位教師教育文憑
      </p>
    </li>
  </ul>
</template>

<script setup>
const openedIndexes = ref([])

const toggle = (index) => {
  console.log("toggle", index)
  if (openedIndexes.value.includes(index)) {
    openedIndexes.value = openedIndexes.value.filter((i) => i !== index)
  } else {
    openedIndexes.value = [...openedIndexes.value, index]
  }
}

const isOpened = (index) => openedIndexes.value.includes(index)

const questions = [
  {
    question: '導師資歷是什麼？',
    answer: '本會導師均為專業幼兒音樂導師，擁有多年豐富幼兒音樂教學經驗及畢業於香港浸會大學、香港教育學院、持音樂學士(音樂教育)、幼兒音樂教育專業證書、 合格幼稚園教師及PGDE 學位教師教育文憑',
  },
  {
    question: '中途退出課程是否可以退款？',
    answer: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus quis ultricies est. Duis nec hendrerit magna. Ut vel orci gravida, hendrerit enim non, gravida turpis. Praesent non lectus porttitor, scelerisque nulla nec, ornare neque. Integer massa libero, ornare ut leo nec, scelerisque rutrum elit. Morbi et massa id ipsum lobortis rhoncus. Aenean sit amet porta nulla, quis varius risus. Suspendisse ultrices ut lectus non laoreet. Etiam ornare laoreet tortor quis porttitor. Suspendisse tempus erat non dui volutpat eleifend.'
  }
]
</script>