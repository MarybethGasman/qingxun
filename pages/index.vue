<template>
  <div id="app" class="p-4 bg-gray-200 min-h-screen">
    <button
      class="
        px-4
        py-2
        mb-4
        text-lg text-white text-semibold
        bg-blue-600
        rounded-md
      "
      @click="add"
    >
      Add new card
    </button>
    <transition-group
      enter-active-class="transform-gpu"
      enter-class="opacity-0 -translate-x-full"
      enter-to-class="opacity-100 translate-x-0"
      leave-active-class="absolute transform-gpu"
      leave-class="opacity-100 translate-x-0"
      leave-to-class="opacity-0 -translate-x-full"
      tag="div"
      class="flex flex-col space-y-4"
      @before-leave="beforeLeave"
    >
      <article
        v-for="(item, index) in items"
        v-bind:key="item"
        class="
          flex
          items-center
          p-4
          bg-white
          rounded-md
          shadow-md
          transition-all
          duration-300
        "
      >
        <div class="flex-1">
          <header class="text-xl text-gray-900 font-semibold">
            {{ `Card #${item}` }}
          </header>
          <div>Card content</div>
        </div>
        <button
          class="p-2 hover:bg-gray-100 rounded-md focus:outline-none"
          @click="remove(index)"
        >
          <svg
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            class="h-6 w-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
            />
          </svg>
        </button>
      </article>
    </transition-group>
  </div>
</template>

<script setup lang="ts">
let items = ref([1, 2, 3, 4, 5, 6, 7, 8, 9].reverse());
let nextNum = ref(10);

let add = function () {
  items.value.unshift(nextNum.value++);
};
let remove = function (index: number) {
  items.value.splice(index, 1);
};
let beforeLeave = (el: HTMLElement) => {
  const { marginLeft, marginTop, width, height } = window.getComputedStyle(el);
  el.style.left = `${el.offsetLeft - parseFloat(marginLeft)}px`;
  el.style.top = `${el.offsetTop - parseFloat(marginTop)}px`;
  el.style.width = width;
  el.style.height = height;
};
</script>
