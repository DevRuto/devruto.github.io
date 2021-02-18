<template>
  <div id="app" class="text-black dark:text-white">
    <Navbar />
    <div class="container flex flex-col space-y-12 mx-auto pt-6 p-4">
      <AboutMe id="AboutMe" />
      <Projects id="Projects" />
      <Contact id="Contact" />
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';
import Contact from './components/Contact.vue';
import Projects from './components/Projects.vue';
import AboutMe from './components/AboutMe.vue';

export default {
  name: 'App',
  components: {
    Navbar,
    Contact,
    Projects,
    AboutMe,
  },
};
</script>
