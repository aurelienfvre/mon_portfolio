<script>
import Navbar from './components/Navbar.vue';

export default {
  name: 'App',
  components: {
    Navbar
  }
};
</script>


<template>
  <div>
    <div class="flex justify-center">
    <Navbar />
  </div>
    <section id="accueil" class="h-screen flex justify-center items-center">
      <h1>Accueil</h1>
    </section>
    <section id="projets" class="h-screen flex justify-center items-center bg-gray-200">
      <h1>Projets</h1>
    </section>
    <section id="contact" class="h-screen flex justify-center items-center bg-gray-400">
      <h1>Contact</h1>
    </section>
  </div>
</template>


