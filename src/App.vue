<template>
  <div class="app">
    <FieldNonograms></FieldNonograms>
  </div>
</template>

<script>
import FieldNonograms from './components/FieldNonograms.vue'
import bcimg from '@/assets/jpg/background-Japan.jpg'

export default {
  name: 'App',
  components: {
    FieldNonograms
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