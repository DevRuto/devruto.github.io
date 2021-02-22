<template>
  <div>
    <div
      class="fixed md:h-3/5 w-full md:w-3/5 md:mx-auto my-auto overflow-hidden z-10 inset-0 pt-20 px-4 pb-4 transition transform duration-200 scale-0"
      :class="{ 'scale-100': selectedProject }"
      >
      <div class="relative bg-gray-100 dark:bg-gray-900 shadow-lg border-2 border-gray-700 overflow-y-auto rounded-lg h-full w-full mx-auto my-auto p-4">
        <div v-if="selectedProject" class="flex flex-col space-y-3">
          <div class="flex flex-row justify-between items-center">
            <div class="text-3xl font-bold">{{ selectedProject.name }}</div>
            <button class="w-8 h-8 focus:outline-none" @click="selectedProject = false">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
          <div class="flex flex-col sm:flex-row sm:space-x-4 space-y-4 sm:space-y-0 divide-dashed">
            <div>
              <div class="font-bold">Description: </div>
              <div class="inline">{{ selectedProject.shortDesc }}</div>
            </div>
            <div>
              <div class="font-bold">Repo: </div>
              <a class="text-blue-500 hover:underline" target="_blank" :href="selectedProject.link">{{ selectedProject.link }}</a>
            </div>
          </div>
          <div class="flex flex-col sm:flex-row pt-4 justify-center sm:justify-start space-y-4 sm:space-y-0 space-x-0 sm:space-x-4">
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
            <div class="flex flex-col border border-gray-700 rounded-lg p-4 w-full sm:w-2/3">
              <div class="font-semibold mx-auto">Summary</div>
              <hr class="border-gray-600 pb-4" />
              <div class="flex flex-col space-y-3">
                <div v-html="selectedProject.longDesc"></div>
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
      <div class="text-xs sm:inline">(select project for details)</div>
    </div>
    <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 space-x-0 sm:space-x-4 pt-4 items-center">
      <div
        class="relative bg-gray-200 dark:bg-gray-600 border-2 rounded-lg border-gray-700 h-40 w-80 p-2 overflow-hidden cursor-pointer hover:bg-gray-300 dark:hover:bg-gray-700"
        v-for="project of projects"
        @click="selectProject(project)"
        :key="project.name">
        <div class="text-xl font-bold text-gray-800 dark:text-gray-200">{{ project.name }}</div>
        <div class="text-sm text-gray-800 dark:text-gray-200">{{ project.shortDesc }}</div>
        <div class="absolute bg-gray-300 dark:bg-gray-400 w-full h-8 bottom-0 left-0"></div>
        <div class="absolute bottom-8 font-mono text-sm">{{ project.language }}</div>
        <div class="absolute bottom-2 left-2">
          <div class="text-white" v-html="project.logo"></div>
        </div>
        <div class="absolute bottom-2 right-2" v-show="project.docker">
          <div class="text-white" v-html="ICON_DOCKER"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const ICON_GITHUB = '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" width="16" height="16"><path fill="currentColor" fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"></path></svg>';
const ICON_BITBUCKET = '<svg width="32" height="32" viewBox="8 -8 32 32" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M9.3201 9.56002C9.0401 9.56002 8.8001 9.80002 8.8801 10.08L10.8401 21.96C10.8801 22.28 11.1601 22.48 11.4401 22.48H20.8401C21.0801 22.48 21.2401 22.32 21.2801 22.08L23.2401 10.04C23.2801 9.76002 23.0801 9.52002 22.8001 9.52002L9.3201 9.56002ZM17.5601 18.16H14.5601L13.7601 13.92H18.2801L17.5601 18.16Z" fill="#2684FF"/><path d="M22.6 13.92H18.28L17.56 18.16H14.56L11.04 22.36C11.04 22.36 11.2 22.52 11.44 22.52H20.84C21.08 22.52 21.24 22.36 21.28 22.12L22.6 13.92Z" fill="url(#paint0_linear)"/><defs><linearGradient id="paint0_linear" x1="23.6137" y1="15.0911" x2="16.4547" y2="20.6793" gradientUnits="userSpaceOnUse"><stop offset="0.176" stop-color="#0052CC"/><stop offset="1" stop-color="#2684FF"/></linearGradient></defs></svg>';
const ICON_GITLAB = '<svg width="32" height="32" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"  viewBox="80 -150 586 559" style="enable-background:new 0 0 586 559;" xml:space="preserve"><style type="text/css"> .st0{fill:#FAFAFA;} .st1{fill:#F0F0F0;} .st2{fill:#FFFFFF;} .st3{fill:#E24329;} .st4{fill:#FCA326;} .st5{fill:#FC6D26;} .st6{fill:#8C929D;} .st7{fill:#2E2E2E;} .st8{fill:none;stroke:#FCA326;stroke-width:16;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;} .st9{fill:none;stroke:#FC6D26;stroke-width:16;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;} .st10{fill:none;stroke:#E24329;stroke-width:16;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;} .st11{fill:none;stroke:#F0F0F0;stroke-miterlimit:10;} .st12{fill:#231F20;} .st13{fill:none;stroke:#231F20;stroke-width:16;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;} .st14{display:none;} .st15{display:inline;opacity:0.1;fill:#E828E3;} .st16{display:inline;} .st17{opacity:0.1;fill:#E828E3;} .st18{font-family: "SourceSansPro-Semibold ";} .st19{font-size:24px;} .st20{display:inline;fill:#DB3B21;} .st21{display:inline;fill:#FC6D26;} .st22{display:inline;fill:#2E2E2E;} .st23{display:inline;fill:#6E49CB;} .st24{display:inline;fill:#380D75;} .st25{display:inline;fill:#FCA121;} .st26{opacity:0.6;fill:none;stroke:#231F20;stroke-width:2;stroke-miterlimit:10;stroke-dasharray:12,6;} .st27{fill:none;stroke:#444444;stroke-width:1.5339;stroke-miterlimit:10;}</style><g id="logo_art"> <g>  <path id="path50_2_" class="st3" d="M293.026,434.983L293.026,434.983l62.199-191.322H230.918L293.026,434.983L293.026,434.983z"   />  <path id="path66_6_" class="st4" d="M143.798,243.662L143.798,243.662l-18.941,58.126c-1.714,5.278,0.137,11.104,4.661,14.394   l163.509,118.801L143.798,243.662L143.798,243.662z"/>  <path id="path74_2_" class="st3" d="M143.798,243.662h87.12l-37.494-115.224c-1.919-5.895-10.282-5.895-12.27,0L143.798,243.662   L143.798,243.662z"/>  <path id="path82_6_" class="st4" d="M442.346,243.662L442.346,243.662l18.873,58.126c1.714,5.278-0.137,11.104-4.661,14.394   L293.026,434.983L442.346,243.662L442.346,243.662z"/>  <path id="path86_2_" class="st3" d="M442.346,243.662h-87.12l37.425-115.224c1.919-5.895,10.282-5.895,12.27,0L442.346,243.662   L442.346,243.662z"/>  <polygon class="st5" points="293.026,434.983 355.225,243.662 442.346,243.662   "/>  <polygon class="st5" points="293.026,434.983 143.798,243.662 230.918,243.662   "/> </g></g><g id="spacing_guides" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns" class="st14"> <path id="path40_18_" sketch:type="MSShapeGroup" class="st15" d="M0,0.5v124h586V0.5H0L0,0.5z"/> <path id="path40_16_" sketch:type="MSShapeGroup" class="st15" d="M0,435.5v124h586v-124H0L0,435.5z"/> <path id="path40_15_" sketch:type="MSShapeGroup" class="st15" d="M462.2,560h124V0h-124V560L462.2,560z"/> <g class="st16">  <text transform="matrix(1 0 0 1 511.2881 283.3319)" class="st18 st19">1x</text> </g> <g class="st16">  <text transform="matrix(1 0 0 1 281.2881 500.9978)" class="st18 st19">1x</text> </g> <g class="st16">  <text transform="matrix(1 0 0 1 281.2881 65.998)" class="st18 st19">1x</text> </g> <path id="path40_5_" sketch:type="MSShapeGroup" class="st15" d="M0,560h124V0H0V560L0,560z"/> <g class="st16">  <text transform="matrix(1 0 0 1 51.2881 283.3319)" class="st18 st19">1x</text> </g></g></svg>';
const ICON_DOCKER = '<svg xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:cc="http://creativecommons.org/ns#" xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#" xmlns:svg="http://www.w3.org/2000/svg" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="80" height="30" viewBox="-10 -50 640 145">   <metadata id="metadata4">     <rdf:RDF>       <cc:Work rdf:about="">         <dc:format>image/svg+xml</dc:format>         <dc:type rdf:resource="http://purl.org/dc/dcmitype/StillImage"/>         <dc:title/>       </cc:Work>     </rdf:RDF>   </metadata>   <defs id="defs6">     <clipPath id="clipPath8">       <path d="m 76,2 0,46 -22,0 0,23 -18.419263,0 c -0.07818,0.665694 -0.141485,1.332869 -0.205737,2 -1.151162,12.530963 1.036422,24.087546 6.0625,33.96875 L 43.125,110 c 1.011403,1.81678 2.191241,3.52297 3.4375,5.1875 1.244725,1.66248 1.685716,2.58262 2.46875,3.6875 C 62.319911,133.81083 82.129473,141 105,141 155.64836,141 198.63299,118.56201 217.65625,68.15625 231.15302,69.54122 244.09968,66.080358 250,54.5625 240.60137,49.138835 228.52163,50.877226 221.5625,54.375 L 240,2 168,48 145,48 145,2 z" id="path10"/>     </clipPath>   </defs>   <path d="m 467.82,113.24092 -0.0422,-25.557862 -0.12687,-45.65718 m 25.85406,19.67617 -25.72712,25.98101 25.85407,25.642492 M 321.28547,88.021573 c 0.12417,-5.480933 -1.46904,-11.08143 -4.69689,-15.613994 -4.65126,-6.53132 -12.17919,-10.9904 -20.43783,-11.08636 -0.55059,0 -1.09558,0 -1.65026,0.04225 -3.26481,0.2017 -6.42662,0.655378 -9.22453,1.819517 -18.40057,7.656 -21.66082,33.207962 -6.13558,44.768575 13.44474,10.01139 33.00155,5.92365 39.77549,-9.351466 1.43144,-3.227887 2.3696,-7.297132 2.3696,-10.578554 l 0,-46.207236 M 445.437,64.367851 c -3.80993,-2.4618 -8.25456,-3.349942 -12.65199,-3.342833 -0.47683,0 -0.96708,0.02383 -1.39637,0.04225 -12.71288,0.54677 -24.50001,9.530355 -24.50001,26.95424 0,20.6003 22.08809,31.71844 38.59069,22.00346 m 74.13473,-2.24266 c 13.00207,-11.1375 39.05614,-33.47058 39.05614,-33.47058 0,0 -0.94989,-1.797148 -1.56563,-2.623492 -5.25739,-7.055515 -13.28929,-10.5786 -21.74957,-10.578627 -20.90871,0 -36.58155,27.0365 -15.74094,46.6727 1.44301,1.35961 3.42523,2.42453 5.62781,3.34283 7.64747,3.18836 18.11655,2.92685 23.78066,-1.26943 M 364.02,61.194275 c -0.59271,0.01083 -1.18194,0.07366 -1.7772,0.08463 -15.85475,0.291353 -27.28615,16.759178 -23.82298,32.031962 3.37478,14.882963 19.63403,23.695883 33.68222,18.829883 16.35859,-4.28927 23.03061,-24.888756 14.04836,-38.802254 -4.9126,-7.60964 -13.23925,-12.3132 -22.1304,-12.14422 z m 240.72631,0.507772 c -6.42012,0.0172 -12.67273,2.265815 -17.30656,6.601038 -7.30767,6.03132 -8.89448,13.64741 -8.80139,23.2729 l 0.21157,21.876522" id="path12" style="fill:none;stroke:#394d54;stroke-width:10.5;stroke-linecap:round;stroke-linejoin:round"/>   <path d="m 147.4876,45.732 22.866,0 0,23.37473 11.56177,0 c 5.33905,0 10.83073,-0.95117 15.887,-2.66444 2.48448,-0.84244 5.27317,-2.01479 7.72392,-3.4892 -3.22785,-4.21436 -4.87579,-9.53574 -5.36101,-14.78106 -0.65874,-7.13426 0.78032,-16.42042 5.60897,-22.004216 l 2.40362,-2.780117 2.8642,2.302393 c 7.21138,5.79374 13.27612,13.88934 14.3451,23.11819 8.68312,-2.55411 18.87759,-1.95 26.53135,2.46735 l 3.14002,1.81182 -1.65276,3.2257 C 246.93289,68.946524 233.40077,72.859896 220.17071,72.167411 200.37356,121.4758 157.2729,144.82 105.01356,144.82 c -26.998899,0 -51.769845,-10.09272 -65.875552,-34.04693 -0.827018,-1.48798 -1.535233,-3.0439 -2.286326,-4.57212 C 32.083548,95.656747 30.499883,84.105687 31.574226,72.564267 l 0.32241,-3.457072 19.552937,0 0,-23.37473 22.866,0 0,-22.866 45.732,0 0,-22.866 27.43967,0 0,45.732" id="path14" style="fill:#394d54"/>   <g clip-path="url(#clipPath8)" id="g16">     <g id="g18">       <g transform="translate(0,-22.866)" id="g20">         <path d="m 123.85901,3.8110794 19.81751,0 0,19.8169706 -19.81751,0 z" id="path22" style="fill:#00acd3"/>         <path d="m 123.85901,26.676485 19.81751,0 0,19.818043 -19.81751,0 z" id="path24" style="fill:#20c2ef"/>         <path d="m 126.29235,21.976904 0,-16.5157492 m 2.97185,16.5157492 0,-16.5157492 m 3.00184,16.5157492 0,-16.5157492 m 3.00344,16.5157492 0,-16.5157492 m 3.00292,16.5157492 0,-16.5157492 m 2.97131,16.5157492 0,-16.5157492" id="path26" style="stroke:#394d54;stroke-width:1.56"/>         <use transform="translate(0,22.866)" id="use28" xlink:href="#path26"/>       </g>       <use transform="matrix(1,0,0,-1,22.866,4.572651)" id="use30" xlink:href="#g20"/>     </g>     <use transform="translate(-91.464,45.732)" id="use32" xlink:href="#g18"/>     <use transform="translate(-45.732,45.732)" id="use34" xlink:href="#g18"/>     <use transform="translate(0,45.732)" id="use36" xlink:href="#g18"/>   </g>   <path d="m 221.57014,54.379649 c 1.53332,-11.915247 -7.38383,-21.274779 -12.91407,-25.71836 -6.37269,7.367765 -7.36295,26.677556 2.63498,34.807431 -5.57952,4.956117 -17.33731,9.448435 -29.37574,9.448435 L 34,72.917155 C 32.829255,85.484184 34,146 34,146 l 217,0 -0.98657,-91.424 c -9.39863,-5.423665 -21.48419,-3.694326 -28.44332,-0.196552" clip-path="url(#clipPath8)" id="path38" style="fill:#17b5eb"/>   <path d="m 34,89 0,57 217,0 0,-57" clip-path="url(#clipPath8)" id="path40" style="fill-opacity:0.17"/>   <path d="M 111.23736,140.88997 C 97.697741,134.4648 90.265707,125.73081 86.130611,116.19562 L 45,118 l 21,28 45.23736,-5.11003" clip-path="url(#clipPath8)" id="path42" style="fill:#d4edf1"/>   <path d="m 222.5,53.9375 0,0.03125 c -20.86119,26.889144 -50.78312,50.37872 -82.90625,62.71875 -28.65478,11.00767 -53.638381,11.06039 -70.875,2.21875 -1.85607,-1.04832 -3.675701,-2.21152 -5.5,-3.3125 C 50.582097,106.76175 43.464274,92.152308 44.0625,72.90625 L 34,72.90625 34,146 l 217,0 0,-96 -25,0 z" clip-path="url(#clipPath8)" id="path44" style="fill-opacity:0.085"/>   <path d="m 45.625,117.03125 c 14.165153,0.77531 29.28245,0.91433 42.46875,-3.21875" id="path46" style="fill:none;stroke:#394d54;stroke-width:3.4;stroke-linecap:round"/>   <path d="m 102.17024,106.95926 c 0,3.01898 -2.447529,5.46651 -5.466508,5.46651 -3.019514,0 -5.467581,-2.44753 -5.467581,-5.46651 0,-3.01897 2.448067,-5.46758 5.467581,-5.46758 3.018979,0 5.466508,2.44861 5.466508,5.46758 z" id="path48" style="fill:#d4edf1"/>   <path d="m 98.121372,103.30778 c -0.477188,0.27582 -0.800133,0.79264 -0.800133,1.3839 0,0.88261 0.715514,1.59706 1.598125,1.59706 0.604653,0 1.130046,-0.3358 1.401576,-0.83174 0.19173,0.4622 0.29831,0.96991 0.29831,1.50226 0,2.16208 -1.752907,3.91498 -3.915518,3.91498 -2.162075,0 -3.91605,-1.7529 -3.91605,-3.91498 0,-2.16314 1.753975,-3.91658 3.91605,-3.91658 0.500218,0 0.977406,0.0943 1.41764,0.2651 z" id="path50" style="fill:#394d54"/>   <path d="m 0,90.162343 254.32743,0 c -5.53774,-1.404786 -17.521,-3.302293 -15.54477,-10.559732 -10.06915,11.651749 -34.35274,8.174326 -40.4812,2.428786 -6.82471,9.89831 -46.55451,6.135967 -49.32553,-1.575096 -8.55565,10.04077 -35.06718,10.04077 -43.62336,0 -2.77209,7.711063 -42.501357,11.473406 -49.326595,1.575096 C 49.897506,87.776937 25.616067,91.25436 15.545841,79.602611 17.522075,86.86005 5.5388117,88.757557 0,90.162343" id="path52" style="fill:#394d54"/> </svg>';

export default {
  data() {
    return {
      selectedProject: false,
      ICON_DOCKER,
      projects: [
        {
          name: 'Portfolio (this site)',
          link: 'https://github.com/DevRuto/devruto.github.io',
          language: 'JavaScript',
          logo: ICON_GITHUB,
          shortDesc: 'My Personal Portfolio',
          longDesc: `
            <p>
              This is the first portfolio. It was pretty fun to make, as I've never made one before.
              The most difficult part of the project was figuring out the design and frameworks I wanted to use.
              Ultimately, I decided to use VueJS, a framework I really enjoyed working with, and TailwindCSS just
              to have more practice with it.
            </p>
            <p class="pt-2">
              Another difficult part of this project was figuring out what to say in the "About Me" section
              of the portfolio.
            </p>
            <p class="pt-2">
              For the first revision of this project, it seems decent to me, but definitely could be a lot better.
              As time goes on, it'll be interesting to see how this portfolio will evolve.
            </p>
          `,
          tools: [
            {
              name: 'Vue.js',
              link: 'https://vuejs.org/',
              desc: 'JavaScript Framework',
            },
            {
              name: 'Vue CLI',
              link: 'https://cli.vuejs.org/',
              desc: 'Vue CLI tool',
            },
            {
              name: 'TailwindCSS',
              link: 'https://tailwindcss.com/',
              desc: 'CSS Framework',
            },
          ],
        },
        {
          name: 'globalapi-portal',
          link: 'https://bitbucket.org/kztimerglobalteam/globalapi-portal',
          language: 'JavaScript',
          docker: true,
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
            {
              name: 'Docker',
              link: 'https://www.docker.com/',
              desc: 'Containerization service for easy application deployment',
            },
          ],
        },
        {
          name: 'Pixel Discord Bot',
          link: 'https://gitlab.com/Ruto/pixel-discord-bot',
          language: 'C#',
          docker: true,
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
            {
              name: 'Docker',
              link: 'https://www.docker.com/',
              desc: 'Containerization service for easy application deployment',
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
