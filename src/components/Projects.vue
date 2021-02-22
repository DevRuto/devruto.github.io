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
        <div class="absolute bottom-2 left-2">
          <div class="text-white" v-html="project.logo"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// const ICON_GITHUB = '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" width="16" height="16"><path fill="currentColor" fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"></path></svg>';
const ICON_BITBUCKET = '<svg width="32" height="32" viewBox="8 -8 32 32" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M9.3201 9.56002C9.0401 9.56002 8.8001 9.80002 8.8801 10.08L10.8401 21.96C10.8801 22.28 11.1601 22.48 11.4401 22.48H20.8401C21.0801 22.48 21.2401 22.32 21.2801 22.08L23.2401 10.04C23.2801 9.76002 23.0801 9.52002 22.8001 9.52002L9.3201 9.56002ZM17.5601 18.16H14.5601L13.7601 13.92H18.2801L17.5601 18.16Z" fill="#2684FF"/><path d="M22.6 13.92H18.28L17.56 18.16H14.56L11.04 22.36C11.04 22.36 11.2 22.52 11.44 22.52H20.84C21.08 22.52 21.24 22.36 21.28 22.12L22.6 13.92Z" fill="url(#paint0_linear)"/><defs><linearGradient id="paint0_linear" x1="23.6137" y1="15.0911" x2="16.4547" y2="20.6793" gradientUnits="userSpaceOnUse"><stop offset="0.176" stop-color="#0052CC"/><stop offset="1" stop-color="#2684FF"/></linearGradient></defs></svg>';
const ICON_GITLAB = '<svg width="32" height="32" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"  viewBox="0 -150 586 559" style="enable-background:new 0 0 586 559;" xml:space="preserve"><style type="text/css"> .st0{fill:#FAFAFA;} .st1{fill:#F0F0F0;} .st2{fill:#FFFFFF;} .st3{fill:#E24329;} .st4{fill:#FCA326;} .st5{fill:#FC6D26;} .st6{fill:#8C929D;} .st7{fill:#2E2E2E;} .st8{fill:none;stroke:#FCA326;stroke-width:16;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;} .st9{fill:none;stroke:#FC6D26;stroke-width:16;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;} .st10{fill:none;stroke:#E24329;stroke-width:16;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;} .st11{fill:none;stroke:#F0F0F0;stroke-miterlimit:10;} .st12{fill:#231F20;} .st13{fill:none;stroke:#231F20;stroke-width:16;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;} .st14{display:none;} .st15{display:inline;opacity:0.1;fill:#E828E3;} .st16{display:inline;} .st17{opacity:0.1;fill:#E828E3;} .st18{font-family: "SourceSansPro-Semibold ";} .st19{font-size:24px;} .st20{display:inline;fill:#DB3B21;} .st21{display:inline;fill:#FC6D26;} .st22{display:inline;fill:#2E2E2E;} .st23{display:inline;fill:#6E49CB;} .st24{display:inline;fill:#380D75;} .st25{display:inline;fill:#FCA121;} .st26{opacity:0.6;fill:none;stroke:#231F20;stroke-width:2;stroke-miterlimit:10;stroke-dasharray:12,6;} .st27{fill:none;stroke:#444444;stroke-width:1.5339;stroke-miterlimit:10;}</style><g id="logo_art"> <g>  <path id="path50_2_" class="st3" d="M293.026,434.983L293.026,434.983l62.199-191.322H230.918L293.026,434.983L293.026,434.983z"   />  <path id="path66_6_" class="st4" d="M143.798,243.662L143.798,243.662l-18.941,58.126c-1.714,5.278,0.137,11.104,4.661,14.394   l163.509,118.801L143.798,243.662L143.798,243.662z"/>  <path id="path74_2_" class="st3" d="M143.798,243.662h87.12l-37.494-115.224c-1.919-5.895-10.282-5.895-12.27,0L143.798,243.662   L143.798,243.662z"/>  <path id="path82_6_" class="st4" d="M442.346,243.662L442.346,243.662l18.873,58.126c1.714,5.278-0.137,11.104-4.661,14.394   L293.026,434.983L442.346,243.662L442.346,243.662z"/>  <path id="path86_2_" class="st3" d="M442.346,243.662h-87.12l37.425-115.224c1.919-5.895,10.282-5.895,12.27,0L442.346,243.662   L442.346,243.662z"/>  <polygon class="st5" points="293.026,434.983 355.225,243.662 442.346,243.662   "/>  <polygon class="st5" points="293.026,434.983 143.798,243.662 230.918,243.662   "/> </g></g><g id="spacing_guides" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns" class="st14"> <path id="path40_18_" sketch:type="MSShapeGroup" class="st15" d="M0,0.5v124h586V0.5H0L0,0.5z"/> <path id="path40_16_" sketch:type="MSShapeGroup" class="st15" d="M0,435.5v124h586v-124H0L0,435.5z"/> <path id="path40_15_" sketch:type="MSShapeGroup" class="st15" d="M462.2,560h124V0h-124V560L462.2,560z"/> <g class="st16">  <text transform="matrix(1 0 0 1 511.2881 283.3319)" class="st18 st19">1x</text> </g> <g class="st16">  <text transform="matrix(1 0 0 1 281.2881 500.9978)" class="st18 st19">1x</text> </g> <g class="st16">  <text transform="matrix(1 0 0 1 281.2881 65.998)" class="st18 st19">1x</text> </g> <path id="path40_5_" sketch:type="MSShapeGroup" class="st15" d="M0,560h124V0H0V560L0,560z"/> <g class="st16">  <text transform="matrix(1 0 0 1 51.2881 283.3319)" class="st18 st19">1x</text> </g></g></svg>';

export default {
  data() {
    return {
      selectedProject: false,
      projects: [
        {
          name: 'globalapi-portal',
          link: 'https://bitbucket.org/kztimerglobalteam/globalapi-portal',
          language: 'javascript',
          logo: ICON_BITBUCKET,
          shortDesc: 'Administrative Portal Front-end',
          longDesc: '',
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
          logo: ICON_GITLAB,
          shortDesc: 'Discord Bot to announce live Twitch Streamers',
          longDesc: '',
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
