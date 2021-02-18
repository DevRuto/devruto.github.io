<template>
  <div class="flex h-2 w-20 outline-none items-center" @click="onToggle">
    <svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
    </svg>
    <div class="relative px-1">
      <div class="bg-gray-200 w-10 h-5 rounded-full"></div>
      <div
        class="absolute w-4 h-4 bg-gray-800 rounded-full inset-y-0.5 left-2 transform transition-all ease-in-out duration-200"
        :class="{ 'translate-x-4': dark }"
      ></div>
    </div>
    <svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
    </svg>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dark: true,
    };
  },
  mounted() {
    if (localStorage.theme === 'dark') {
      this.dark = true;
    } else {
      this.dark = false;
    }
    this.setTheme();
  },
  methods: {
    onToggle() {
      this.dark = !this.dark;
      this.setTheme();
    },
    setTheme() {
      if (this.dark) {
        document.documentElement.classList.add('dark');
        localStorage.theme = 'dark';
      } else {
        document.documentElement.classList.remove('dark');
        localStorage.removeItem('theme');
      }
    },
  },
};
</script>
