<template>
  <div class="app">
    <NameNonograms msg="Welcome to Your Vue.js App"></NameNonograms>
  </div>
</template>

<script>
import NameNonograms from './components/NameNonograms.vue'
import bcimg from '@/assets/jpg/background-Japan.jpg'

export default {
  name: 'App',
  components: {
    NameNonograms
  },
  data() {
    return {
      bcimg: bcimg
    }
  }
}
</script>

<style scoped>
.app {
  background-image: url(@/assets/jpg/background-Japan.jpg);
  display: flex;
  justify-content: center;
  align-items: center;
  background-repeat: no-repeat;
  height: 100vh;
  background-size: contain;
  background-position: center;
}

.app img {
  width: 100%;
  height: 100vh;
}

</style>