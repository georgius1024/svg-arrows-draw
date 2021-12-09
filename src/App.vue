<template>
  <template v-if="points.length">
    <template v-for="(point, index) in points">
      <span
        :style="{
          position: 'absolute',
          left: `${point.x - 2}px`,
          top: `${point.y - 2}px`,
          width: '4px',
          height: '4px',
          background: 'black',
          borderRadius: '100%',
          zIndex: 1000,
        }"
      ></span>
      <Connector
        v-if="index > 0"
        :fromX="points[index - 1].x"
        :fromY="points[index - 1].y"
        :toX="point.x"
        :toY="point.y"
        :stroke="12"
      />
    </template>
    <template v-if="current.x">
      <Connector
        :fromX="points[points.length - 1].x"
        :fromY="points[points.length - 1].y"
        :toX="current.x"
        :toY="current.y"
        :stroke="12"
      />
    </template>
  </template>
  <template v-else>
    <div
      style="
        width: 100vw;
        height: 100vh;
        position: absolute;
        display: flex;
        align-items: center;
        justify-content: center;
      "
    >
      Click to start path
    </div>
  </template>
  <!-- {{mouseX}}x{{mouseY}}
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
  ></span> -->
</template>

<script>
import Connector from "./components/Connector.vue";
export default {
  components: {
    Connector,
  },
  data() {
    return {
      points: [],
      current: {},
    };
  },
  mounted() {
    this.mouseUpListener = (e) => {
      this.points.push(this.snapped({ x: e.pageX, y: e.pageY }));
    };
    this.mouseMoveListener = (e) => {
      this.current = this.snapped({ x: e.pageX, y: e.pageY });
    };
    document.addEventListener("mouseup", this.mouseUpListener);
    document.addEventListener("mousemove", this.mouseMoveListener);
  },
  beforeUnmount() {
    document.removeEventListener("mouseup", this.mouseUpListener);
    document.removeEventListener("mousemove", this.mouseMoveListener);
  },
  methods: {
    snapToGrid(value, step = 50) {
      return Math.round(value / step) * step;
    },
    snapped(point) {
      const { x, y } = point;
      return {
        x: this.snapToGrid(x),
        y: this.snapToGrid(y),
      };
    },
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
