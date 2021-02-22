<template>
  <div id="app" class="flex flex-col h-screen overflow-y-auto text-black dark:text-white transition">
    <Navbar />
    <div class="container flex-grow flex flex-col space-y-12 mx-auto pt-6 p-4 z-0">
      <AboutMe id="AboutMe" />
      <Projects id="Projects" />
      <Contact id="Contact" />
    </div>
    <Footer />
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';
import Contact from './components/Contact.vue';
import Projects from './components/Projects.vue';
import AboutMe from './components/AboutMe.vue';
import Footer from './components/Footer.vue';

export default {
  name: 'App',
  components: {
    Navbar,
    Contact,
    Projects,
    AboutMe,
    Footer,
  },
};
</script>
