<template>
  <div class="w-full h-full p-4 flex justify-center items-center">
    <div class="max-w-md">
      <div>
        <img src="/assets/tree.svg" alt="Christmas tree" />
      </div>
      <div class="mt-2 flex justify-center items-center">
        <img
          v-for="present in sortedPresents"
          :key="present.id"
          :src="present.src"
          :alt="`Present ${present.id}`"
          data-qa="present"
        />
      </div>
      <button
        class="bg-slate-900 hover:bg-slate-700 focus:outline-none focus:ring-2 focus:ring-slate-400 focus:ring-offset-2 focus:ring-offset-slate-50 text-white font-semibold h-12 px-6 rounded-lg flex items-center justify-center mx-auto mt-8"
        @click="isSorted = !isSorted"
      >
        Toggle sort
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import presents from './presents.json'

const isSorted = ref(false)

const sortedPresents = computed(() => {
  if (isSorted.value) {
    const sortList = [...presents]
    return sortList.sort((a, b) => getDimensions(a.dimensions) - getDimensions(b.dimensions))
  }

  return presents
})

const getDimensions = ({ height, width }) => {
  return height * width
}
</script>
