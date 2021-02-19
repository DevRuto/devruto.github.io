<template>
  <div class="bg-gray-600 w-full font-mono">
    <div class="container flex flex-col sm:flex-row justify-between h-16 mx-auto">
      <div class="bg-gray-600 flex items-center justify-between h-full z-50 px-4 pt-4 sm:pt-0">
        <div class="text-white font-medium text-3xl">Winston<div class="text-xs inline"> aka</div><div class="text-sm inline"> Ruto</div></div>
        <button class="sm:hidden w-8 h-8 text-white focus:outline-none" @click="collapse = !collapse">
          <svg v-show="collapse" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z" clip-rule="evenodd" />
          </svg>
          <svg v-show="!collapse" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd" />
          </svg>
        </button>
      </div>
      <div
        :class="{ '-translate-y-60 sm:translate-y-0': collapse }"
        class="flex flex-col items-center sm:flex-row space-y-3 sm:space-y-0 sm:space-x-6 text-white px-4 transform transition-all ease-in-out duration-200 bg-gray-600 py-6 sm:py-4 z-40">
        <a class="text-lg transition-colors hover:text-purple-400 focus:text-purple-500" href="#AboutMe" @click="collapse = true">About Me</a>
        <a class="text-lg transition-colors hover:text-purple-400 focus:text-purple-500" href="#Projects" @click="collapse = true">Projects</a>
        <a class="text-lg transition-colors hover:text-purple-400 focus:text-purple-500" href="#Contact" @click="collapse = true">Contact</a>
        <a class="transition-colors hover:text-purple-200 focus:text-purple-400" href="https://github.com/devruto">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" width="20" height="20"><path fill="currentColor" fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"></path></svg>
        </a>
        <ThemeSwitch class="pt-4 sm:pt-0" />
      </div>
    </div>
  </div>
</template>

<script>
import ThemeSwitch from './ThemeSwitch.vue';

export default {
  components: {
    ThemeSwitch,
  },
  data() {
    return {
      collapse: true,
    };
  },
};
</script>
