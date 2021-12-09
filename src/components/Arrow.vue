<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    :width="width"
    :height="height"
    :viewBox="viewBox"
    :style="style"
  >
    <marker
      id="dot"
      viewBox="0 0 10 10"
      refX="1"
      refY="5"
      markerUnits="strokeWidth"
      markerHeight="2"
      orient="auto"
    >
      <circle cx="5" cy="5" r="5" />
    </marker>

    <marker
      id="triangle"
      viewBox="0 0 10 10"
      refX="1"
      refY="5"
      markerUnits="strokeWidth"
      markerHeight="3"
      orient="auto"
    >
      <path d="M 0 0 L 10 5 L 0 10 z" />
    </marker>
    <line
      :x1="x1"
      :y1="y1"
      :x2="x2"
      :y2="y2"
      marker-start="url(#dot)"
      marker-end="url(#triangle)"
      stroke="red"
      :stroke-width="stroke"
    />
  </svg>
</template>
<script>
export default {
  props: ["fromX", "fromY", "toX", "toY", "stroke"],
  computed: {
    width() {
      return 500; //Math.max(Math.abs(this.fromX - this.toX), this.stroke * 3);
    },
    height() {
      return 500; //Math.max(Math.abs(this.fromY - this.toY), this.stroke * 3);
    },
    viewBox() {
      return `0 0 ${this.width} ${this.height}`;
    },
    offset() {
      return this.stroke * 3;
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
    left() {
      return this.fromX < this.toX ? this.fromX : this.fromX - this.width;
    },
    top() {
      return this.fromY < this.toY ? this.fromY : this.fromY - this.height;
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
