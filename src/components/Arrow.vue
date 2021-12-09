<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    :width="width"
    :height="height"
    :viewBox="viewBox"
    :style="style"
  >
    <rect
      :x="0"
      :y="0"
      :width="width"
      :height="height"
      stroke="black"
      fill="white"
      stroke-width="1"
    />
    <!-- <circle
      :cx="x1"
      :cy="y1"
      :r="stroke - 1"
      stroke="black"
      fill="white"
      stroke-width="2"
    />
    <circle
      :cx="x2"
      :cy="y2"
      :r="stroke - 1"
      stroke="black"
      fill="white"
      stroke-width="2"
    /> -->
    <!-- <marker
      id="dot"
      viewBox="0 0 10 10"
      refX="1"
      refY="5"
      markerUnits="strokeWidth"
      markerHeight="2"
      orient="auto"
    >
      <circle cx="5" cy="5" r="4"  stroke="black" fill="white" stroke-width="2" />
    </marker>

    <marker
      id="triangle"
      viewBox="0 0 20 20"
      refX="1"
      refY="5"
      markerUnits="strokeWidth"
      markerHeight="4"
      orient="auto"
    >
      <path d="M 0 0 L 10 5 L 0 10 z" />
      <circle cx="15" cy="5" r="4" stroke="black" fill="white" stroke-width="2"/>
    </marker>
    <line
      :x1="x1"
      :y1="y1"
      :x2="x2"
      :y2="y2"
      marker-start="url(#dot)"
      marker-end="url(#triangle)" -->
    stroke="red" :stroke-width="stroke" /> -->
  </svg>
</template>
<script>
export default {
  props: ["fromX", "fromY", "toX", "toY", "stroke"],
  computed: {
    minWidth() {
      return this.stroke * 3
    },
    padding() {
      this.stroke / 2
    },
    angle() {
      return Math.atan((this.fromX - this.toX)/(this.toY - this.fromY))
    },
    corners() {
      
    },
    left() {
      return this.fromX < this.toX ? this.fromX : this.fromX - this.width;
    },
    top() {
      return this.fromY < this.toY ? this.fromY : this.fromY - this.height;
    },
    width() {
      return Math.max(Math.abs(this.fromX - this.toX), this.stroke * 3);
    },
    height() {
      return Math.max(Math.abs(this.fromY - this.toY), this.stroke * 3);
    },
    viewBox() {
      return `${-this.stroke} ${-this.stroke} ${this.width + 2 * this.stroke} ${
        this.height + 2 * this.stroke
      }`;
    },
    offset() {
      return this.stroke * 1.5;
    },
    x1() {
      return this.fromX < this.toX ? this.offset : this.width - this.offset;
    },
    y1() {
      return this.fromY < this.toY ? this.offset : this.height - this.offset;
    },
    x2() {
      return this.fromX < this.toX ? this.width - this.offset : this.offset;
    },
    y2() {
      return this.fromY < this.toY ? this.height - this.offset : this.offset;
    },
    // x1() {
    //   return this.fromX < this.toX ? this.offset : this.width - this.offset;
    // },
    // y1() {
    //   return this.fromY < this.toY ? this.offset : this.height - this.offset;
    // },
    // x2() {
    //   return this.fromX < this.toX ? this.width - this.offset : this.offset;
    // },
    // y2() {
    //   return this.fromY < this.toY ? this.height - this.offset : this.offset;
    // },

    // x1() {
    //   return this.fromX < this.toX ? 10 : this.width - 20;
    // },
    // y1() {
    //   return this.fromY < this.toY ? 10 : this.height - 20;
    // },
    // x2() {
    //   return this.fromX < this.toX ? this.width - 20 : 10;
    // },
    // y2() {
    //   return this.fromY < this.toY ? this.height - 20 : 10;
    // },
    style() {
      return {
        position: "absolute",
        left: `${this.left}px`, // XY needs to be improved for other quadrant
        top: `${this.top}px`,
        // left: `${Math.min(this.fromX, this.toX)}px`,
        // top: `${Math.min(this.fromY, this.toY)}px`,
      };
    },
  },
};
</script>
