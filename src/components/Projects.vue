<template>
  <div>
    <div v-if="selectedProject" class="fixed h-full w-full md:h-2/3 md:w-2/3 md:mx-auto md:my-auto z-10 inset-0 pt-20 px-4 pb-4">
      <div class="bg-blue-400 rounded h-full w-full mx-auto my-auto p-4">
        modal
      </div>
    </div>
    <div class="text-4xl font-mono">
      <a class="inline-block" href="#Projects">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" width="20" height="20"><path fill="currentColor" fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg>
      </a>
      Projects
    </div>
    <div class="flex flex-col">
      <div
        class="border-2 rounded-lg border-gray-200 h-40 w-60 p-2 overflow-hidden"
        v-for="project of projects"
        @click="selectProject(project)"
        :key="project.name">
        <div class="text-xl font-bold">{{ project.name }}</div>
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
