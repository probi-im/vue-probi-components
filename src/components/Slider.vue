<template>
  <div
    class="probi-slider"
    :class="[size ? size : '']"
    @mousedown="startMove"
    @mouseup="endMove"
    @mouseleave="endMove"
    @mousemove="mouseMove"
  >
    <div ref="rail" class="rail" :style="{ backgroundColor }">
      <div
        ref="progress"
        class="progress"
        :style="{ width: percent + '%', backgroundColor: fillColor }"
      ></div>
      <button
        ref="thumb"
        class="thumb"
        :style="{ left: percent + '%', backgroundColor: fillColor }"
      ></button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProbiSlider',
  props: {
    backgroundColor: {
      type: String,
      default: 'lightgray',
    },
    fillColor: {
      type: String,
      default: 'orange',
    },
    lazy: {
      type: Boolean,
      default: false,
    },
    size: {
      type: String,
      default: '',
      validate: (v) => ['small', 'large'].includes(v),
    },
    value: {
      type: Number,
      default: 0,
      validate: (v) => v >= 0 && v <= 100,
    },
  },
  computed: {
    minCursorLeft() {
      return 0;
    },
    percent() {
      return !this.mousePressed ? this.value : this.cursorPos;
    },
  },
  data() {
    return {
      mousePressed: false,
      cursorPos: this.value >= 0 && this.value <= 100 ? this.value : 0,
    };
  },
  methods: {
    startMove(e) {
      if (this.mousePressed) return;
      this.mousePressed = true;
      this.mouseMove(e);
    },
    endMove() {
      if (!this.mousePressed) return;
      this.mousePressed = false;
      if (this.lazy) this.$emit('update:value', this.cursorPos);
    },
    mouseMove(e, force = false) {
      if (!this.mousePressed && !force) return;
      const railOffset = this.$refs.rail.getBoundingClientRect().x;
      const x = Math.max(e.x - railOffset, 0);
      const railWidth = this.$refs.rail.getBoundingClientRect().width;
      this.cursorPos = Math.min((x * 100) / railWidth, 100);
      if (!this.lazy) this.$emit('update:value', this.cursorPos);
    },
  },
};
</script>

<style lang="scss" scoped>
.probi-slider {
  width: 300px;
  padding: 5px 10px;
  display: flex;
  align-items: center;

  &.small {
    height: 9px;
    padding: 3px 6px;

    .rail {
      height: 5px;

      .thumb {
        width: 15px;
        height: 15px;
        border-width: 2px;
      }
    }
  }
  &.large {
    height: 30px;
    padding: 10px 20px;

    .rail {
      height: 15px;

      .thumb {
        width: 25px;
        height: 25px;
        border-width: 4px;
      }
    }
  }

  .rail {
    width: 100%;
    height: 10px;
    position: relative;
    border-radius: 10px;

    .progress {
      height: 100%;
      border-radius: inherit;
    }
    .thumb {
      position: absolute;
      top: 50%;
      width: 20px;
      height: 20px;
      border: none;
      border-radius: 20px;
      transform: translate(-50%, -50%);
      padding: 0;
      outline: none;
      pointer-events: none;
    }
  }
}
</style>