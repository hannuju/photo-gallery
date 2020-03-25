<template>
  <div id="app">
    <PageHeading title="Photo Gallery"/>
    <HeroImage/>
    <Gallery/>
    <BottomLinks/>
  </div>
</template>

<script>
import PageHeading from './components/PageHeading.vue'
import HeroImage from './components/HeroImage.vue'
import Gallery from './components/Gallery.vue'
import BottomLinks from './components/BottomLinks.vue'

export default {
  name: 'App',
  components: {
    PageHeading,
    HeroImage,
    Gallery,
    BottomLinks
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ccc7ba;
  margin-top: 60px;
}
body {
  background-color: #1c1c1c;
}
</style>
