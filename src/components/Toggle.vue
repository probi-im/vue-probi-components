<template>
  <label class="probi-toggle" :style="{ '--scale': toggleScale }">
    <input type="checkbox" v-model="inputValue" />
    <span class="slider round"></span>
  </label>
</template>

<script>
export default {
  name: 'ProbiToggle',
  props: {
    outlined: {
      type: Boolean,
      default: false,
    },
    size: {
      type: String,
      default: '',
    },
    value: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    inputValue: {
      get() {
        return this.value;
      },
      set(value) {
        this.$emit('input', value);
      },
    },
    toggleScale() {
      switch (this.size) {
        case 'x-small':
          return 0.5;
          break;
        case 'small':
          return 0.75;
          break;
        case 'large':
          return 1.25;
          break;
        case 'x-large':
          return 1.5;
          break;
        default:
          return 1;
          break;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.probi-toggle {
  --scale: 1;
  --slider-size: calc(24px * var(--scale));
  --gap-size: calc(4px * var(--scale));
  --transition-duration: 0.1s;
  position: relative;
  display: inline-block;
  height: calc(var(--gap-size) * 2 + var(--slider-size));
  width: calc(var(--gap-size) * 2 + var(--slider-size) * 2);

  input {
    opacity: 0;
    width: 0;
    height: 0;
  }

  .slider {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #ccc;
    cursor: pointer;
    transition: calc(var(--transition-duration) * 3);

    &:before {
      position: absolute;
      content: '';
      top: var(--gap-size);
      bottom: var(--gap-size);
      left: var(--gap-size);
      right: 50%;
      background-color: #fff;
      transition: left var(--transition-duration),
        right var(--transition-duration) var(--transition-duration);
    }
    &:hover {
      background-color: #9abeff;
    }

    &.round {
      border-radius: var(--slider-size);

      &:before {
        border-radius: var(--slider-size);
      }
    }
  }

  input:checked + .slider {
    background-color: #2974ff;
  }
  input:checked + .slider:before {
    left: 50%;
    right: var(--gap-size);
    transition: right var(--transition-duration),
      left var(--transition-duration) var(--transition-duration);
  }
}
</style>