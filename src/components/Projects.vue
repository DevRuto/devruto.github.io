<template>
  <div>
    <div
      class="fixed h-2/3 md:h-1/2 w-full md:w-3/5 md:mx-auto my-auto overflow-hidden z-10 inset-0 pt-20 px-4 pb-4 transition transform duration-200 scale-0"
      :class="{ 'scale-100': selectedProject }"
      >
      <div class="relative bg-gray-100 dark:bg-gray-900 shadow-lg border-2 border-gray-700 overflow-y-auto rounded-lg h-full w-full mx-auto my-auto p-4">
        <div v-if="selectedProject" class="flex flex-col">
          <div class="flex flex-row justify-between items-center">
            <div class="text-3xl font-bold">{{ selectedProject.name }}</div>
            <button class="w-8 h-8 focus:outline-none" @click="selectedProject = false">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
          <a class="text-blue-500 hover:underline" target="_blank" :href="selectedProject.link">{{ selectedProject.link }}</a>
          <div class="flex flex-col sm:flex-row pt-4 justify-center sm:justify-start space-y-4 sm:space-y-0 space-x-0 sm:space-x-4">
            <div class="flex flex-col border border-gray-700 rounded-lg p-4">
              <div class="font-semibold mx-auto">Description</div>
              <hr class="border-gray-600 pb-4" />
              <div class="">
                {{ selectedProject.shortDesc }}
              </div>
            </div>
            <div class="flex flex-col border border-gray-700 rounded-lg p-4">
              <div class="font-semibold mx-auto">Technologies</div>
              <hr class="border-gray-600 pb-4" />
              <div class="flex flex-col space-y-3">
                <div v-for="tool of selectedProject.tools" :key="tool.name">
                  <a class="text-blue-500 hover:underline" :href="tool.link" target="_blank">{{ tool.name }}</a>
                  - {{ tool.desc }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="text-4xl font-mono">
      <a class="inline-block" href="#Projects">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" width="20" height="20"><path fill="currentColor" fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg>
      </a>
      Projects
    </div>
    <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 space-x-0 sm:space-x-4 pt-4">
      <div
        class="relative bg-gray-200 dark:bg-gray-700 border-2 rounded-lg border-gray-500 h-40 w-60 p-2 overflow-hidden cursor-pointer hover:bg-gray-300 dark:hover:bg-gray-600"
        v-for="project of projects"
        @click="selectProject(project)"
        :key="project.name">
        <div class="text-xl font-bold text-gray-800 dark:text-gray-200">{{ project.name }}</div>
        <div class="text-sm text-gray-800 dark:text-gray-200">{{ project.shortDesc }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedProject: false,
      projects: [
        {
          name: 'globalapi-portal',
          link: 'https://bitbucket.org/kztimerglobalteam/globalapi-portal',
          language: 'javascript',
          shortDesc: 'Administrative Portal Front-end',
          tools: [
            {
              name: 'Vue.js',
              link: 'https://vuejs.org/',
              desc: 'JavaScript Framework',
            },
            {
              name: 'Nuxt.js',
              link: 'https://nuxtjs.org/',
              desc: 'Vue Framework',
            },
            {
              name: 'Vuetify',
              link: 'https://vuetifyjs.com/',
              desc: 'Material Design Framework',
            },
          ],
        },
        {
          name: 'Pixel Discord Bot',
          link: 'https://gitlab.com/Ruto/pixel-discord-bot',
          language: 'C#',
          shortDesc: 'Discord Bot to announce live Twitch Streamers',
          tools: [
            {
              name: '.NET 5',
              link: 'https://docs.microsoft.com/en-us/dotnet/core/dotnet-five',
              desc: '.NET Framework',
            },
            {
              name: 'Discord.Net',
              link: 'https://github.com/discord-net/Discord.Net',
              desc: '.NET API Wrapper for Discord',
            },
            {
              name: 'NLog',
              link: 'https://nlog-project.org/',
              desc: 'Logging Framework for .NET',
            },
          ],
        },
      ],
    };
  },
  methods: {
    selectProject(project) {
      this.selectedProject = project;
    },
  },
};
</script>
