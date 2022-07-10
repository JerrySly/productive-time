<template>
  <svg :width="width" :height="height" viewBox="0 0 128 128">
    <g  :fill="color">
      <line
        :fill="color"
        style="
          stroke: #3d883d;
          stroke-width: 12;
          stroke-linecap: square;
          stroke-miterlimit: 10;
        "
        x1="111"
        x2="64"
        y1="40.5"
        y2="87.499"
      />
      <line
        :fill="color"
        
        style="
          stroke: #3d883d;
          stroke-width: 12;
          stroke-linecap: square;
          stroke-miterlimit: 10;
        "
        x1="64"
        x2="17"
        y1="87.499"
        y2="40.5"
      />
    </g>
  </svg>
</template>

<script>
export default {
  props: {
    width: {
      type: String,
      default: "32px",
    },
    height: {
      type: String,
      default: "32px",
    },
    color: {
      type: String,
      default: "#3d883d",
    },
  },
};
</script>

<style>
</style>