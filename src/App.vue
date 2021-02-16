<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <AboutMe />
    <Projects />
    <Contact />
  </div>
</template>

<script>
import Contact from './components/Contact.vue';
import Projects from './components/Projects.vue';
import AboutMe from './components/AboutMe.vue';

export default {
  name: 'App',
  components: {
    Contact,
    Projects,
    AboutMe,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
