<template>
  {{mouseX}}x{{mouseY}}
  <Arrow
    :fromX="originX"
    :fromY="originY"
    :toX="mouseX"
    :toY="mouseY"
    :stroke="12"
  />
  <span
    :style="{
      position: 'absolute',
      left: `${originX - 2}px`,
      top: `${originY - 2}px`,
      width: '4px',
      height: '4px',
      background: 'black',
      borderRadius: '100%',
      zIndex: 1000
    }"
  ></span>
  <span
    :style="{
      position: 'absolute',
      left: `${mouseX - 2}px`,
      top: `${mouseY - 2}px`,
      width: '4px',
      height: '4px',
      background: 'black',
      borderRadius: '100%',
      zIndex: 1000
    }"
  ></span>
</template>

<script>
import Arrow from "./components/Arrow.vue";
export default {
  components: {
    Arrow,
  },
  data() {
    return {
      originX: 600,
      originY: 400,
      mouseX: 150,
      mouseY: 800,
    };
  },
  mounted() {
    this.mouseListener = (e) => {
      this.mouseX = e.pageX;
      this.mouseY = e.pageY;
    };
    document.addEventListener('mousemove', this.mouseListener)
  },
  beforeUnmount() {
    document.removeEventListener("mousemove", this.mouseListener);
  },
};
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  height: 100vh;
  position: relative;
}
</style>
