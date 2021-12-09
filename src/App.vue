<template>
  <Arrow :fromX="originX" :fromY="originY" :toX="mouseX" :toY="mouseY" :stroke="12"/>
</template>

<script>
import Arrow from './components/Arrow.vue'
export default {
  components: {
    Arrow
  },
  data() {
    return {
      originX: 800,
      originY: 600,
      mouseX: 100,
      mouseY: 100
    }
  },
  mounted() {
    this.mouseListener = (e) => {
      this.mouseX = e.pageX
      this.mouseY = e.pageY
    }
    document.addEventListener('mousemove', this.mouseListener)
  },
  beforeUnmount() {
    document.removeEventListener('mousemove', this.mouseListener)
  }
};
</script>


<style>
html, body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  height: 100vh;
  position: relative;;
}
</style>
