<template>
  <div id="app">
    <Navbar />
    <div class="container">
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
