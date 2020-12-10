<template>
  <span class="probi-loader" :style="{ width: width + 'px' }">
    <svg class="circular" viewBox="25 25 50 50">
      <circle
        class="path"
        cx="50"
        cy="50"
        r="20"
        fill="none"
        :stroke-width="strokeWidth"
        stroke-miterlimit="10"
      />
    </svg>
  </span>
</template>

<script>
export default {
  name: 'ProbiLoader',
  props: {
    strokeWidth: {
      type: Number,
      default: 3,
    },
    width: {
      type: Number,
      default: 30,
    },
  },
};
</script>

<style lang="scss" scoped>
.probi-loader {
  // credit: https://codemyui.com/material-design-google-loader-in-css/
  position: relative;

  &:before {
    content: '';
    display: block;
    padding-top: 100%;
  }
}

.circular {
  animation: rotate 2s linear infinite;
  height: 100%;
  transform-origin: center center;
  width: 100%;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
}

.path {
  stroke-dasharray: 1, 200;
  stroke-dashoffset: 0;
  animation: dash 1.5s ease-in-out infinite;
  stroke-linecap: round;
  stroke: #2974ff;
}

@keyframes rotate {
  100% {
    transform: rotate(360deg);
  }
}

@keyframes dash {
  0% {
    stroke-dasharray: 1, 200;
    stroke-dashoffset: 0;
  }
  50% {
    stroke-dasharray: 89, 200;
    stroke-dashoffset: -35px;
  }
  100% {
    stroke-dasharray: 89, 200;
    stroke-dashoffset: -124px;
  }
}
</style>