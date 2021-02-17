<template>
  <div class="bg-gray-600 w-full font-mono">
    <div class="container flex flex-col sm:flex-row justify-between h-16 mx-auto">
      <div class="bg-gray-600 flex items-center justify-between h-full z-50 px-4 pt-4 sm:pt-0">
        <div class="text-white font-bold text-xl">Winston</div>
        <button class="sm:hidden w-8 h-8 text-white" @click="collapse = !collapse">
          <svg v-show="collapse" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z" clip-rule="evenodd" />
          </svg>
          <svg v-show="!collapse" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd" />
          </svg>
        </button>
      </div>
      <div
        :class="{ '-translate-y-48 sm:translate-y-0': collapse }"
        class="flex flex-col sm:flex-row space-y-3 sm:space-x-6 text-white px-4 transform transition-all ease-in-out duration-200 bg-gray-600 py-6 sm:py-4">
        <a class="text-lg transition-colors hover:text-purple-200 focus:text-purple-400" href="#AboutMe">About Me</a>
        <a class="text-lg transition-colors hover:text-purple-200 focus:text-purple-400" href="#Projects">Projects</a>
        <a class="text-lg transition-colors hover:text-purple-200 focus:text-purple-400" href="#Contact">Contact</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      collapse: true,
    };
  },
};
</script>
