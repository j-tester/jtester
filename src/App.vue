<template>
  <div id="app">
    <Navigation />
    <main>
      <router-view/>
    </main>
    <Footer />
  </div>
</template>

<style lang="scss">
@import '@/assets/css/app.scss';
</style>

<script>
import Navigation from '@/components/Navigation.vue';
import Footer from '@/components/Footer.vue';

export default {
  name: 'app',
  components: {
    Navigation,
    Footer,
  },
};
</script>
