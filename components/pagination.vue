<template>
  <nav aria-label="Page navigation" v-if="showdata">
    <div class="inline-flex space-x-2">
      <button
        class="flex items-center justify-center w-10 h-10 transition-colors duration-150 rounded-full focus:shadow-outline"
        :disabled="!hasPrevious"
        :class="!hasPrevious ? 'text-neutral-500' : 'hover:bg-blue-100 text-blue-800'"
        @click="toPreviousPage"
      >
        <svg class="w-4 h-4 fill-current" viewBox="0 0 20 20">
          <path
            d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
            clip-rule="evenodd"
            fill-rule="evenodd"
          ></path>
        </svg>
      </button>
      <template v-for="page in pageCount" :key="data.current_page">
        <button
          v-if="displayButton(page, data.current_page)"
          @click="toPage(page)"
          class="w-10 h-10 transition-colors duration-150 rounded-full focus:shadow-outline"
          :class="
            page === data.current_page
              ? 'text-white bg-blue-800 border border-r-0 border-blue-800 hover:bg-blue-700'
              : 'text-blue-800 hover:bg-blue-100'
          "
        >
          {{ page }}
        </button>
      </template>
      <button
        class="flex items-center justify-center w-10 h-10 transition-colors duration-150 rounded-full focus:shadow-outline"
        :disabled="!hasNext"
        :class="!hasNext ? 'text-neutral-500' : 'hover:bg-blue-100 text-blue-800'"
        @click="toNextPage"
      >
        <svg class="w-4 h-4 fill-current" viewBox="0 0 20 20">
          <path
            d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
            clip-rule="evenodd"
            fill-rule="evenodd"
          ></path>
        </svg>
      </button>
    </div>
  </nav>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
  setup(props) {
    const router = useRouter();
    const pageCount = Math.ceil(props.data.total / props.data.per_page);

    const hasPrevious = computed(() => {
      return props.data.current_page > 1;
    });

    const hasNext = computed(() => {
      return props.data.current_page < pageCount;
    });

    const showdata = computed(() => {
      return pageCount > 1;
    });
    return { router, pageCount, hasPrevious, hasNext, showdata };
  },
  methods: {
    toNextPage() {
      console.log(this.data.current_page);
      if (this.hasNext) {
        navigateTo({
          query: {
            page: this.data.current_page + 1,
          },
        });
        this.$emit("page", this.data.current_page + 1);
      }
    },
    toPreviousPage() {
      if (this.hasPrevious) {
        navigateTo({
          query: {
            page: this.data.current_page - 1,
          },
        });
        this.$emit("page", this.data.current_page - 1);
        console.log(this.data);
      }
    },
    toPage(page) {
      if (page != this.data.current_page) {
        navigateTo({
          query: {
            page: page,
          },
        });
        this.$emit("page", page);
        console.log(this.data);
      }
    },
    displayButton(page, currentPage) {
      if (currentPage == 1 || currentPage == this.pageCount) {
        if (page < currentPage + 5 && page > currentPage - 5) {
          return true;
        } else {
          return false;
        }
      } else if (currentPage == 2 || currentPage == this.pageCount - 1) {
        if (page < currentPage + 4 && page > currentPage - 4) {
          return true;
        } else {
          return false;
        }
      } else {
        if (page < currentPage + 3 && page > currentPage - 3) {
          return true;
        } else {
          return false;
        }
      }
    },
  },
};
</script>
