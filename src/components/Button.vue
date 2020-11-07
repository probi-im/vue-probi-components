<template>
  <button
    class="probi-button "
    :class="[
      'probi-button-' + color,
      outlined ? 'probi-button-outlined' : '',
      rounded ? 'probi-button-rounded' : '',
      size ? 'probi-button-' + size : ''
    ]"
  >
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'ProbiButton',
  props: {
    color: {
      type: String,
      default: 'primary',
      validate: v => ['primary', 'secondary', 'accent'].includes(v)
    },
    outlined: {
      type: Boolean,
      default: false
    },
    rounded: {
      type: Boolean,
      default: true
    },
    size: {
      type: String,
      default: '',
      validate: v => ['small', 'large'].includes(v)
    }
  }
};
</script>

<style lang="scss">
@use "sass:map";
@import '@/assets/scss/variables';

.probi-button {
  outline: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 10px;
  background: none;
  border: none;
  transition: 0.2s background ease;
  font-size: 1.1em;
  min-width: 30px;
  min-height: 30px;

  &:hover {
    cursor: pointer;
  }
  &-outlined {
    border-width: 1px;
    border-style: solid;
    background: none;
  }
  &-rounded {
    border-radius: 7px;
  }
  &-small {
    padding: 7px;
    font-size: 0.8em;
  }
  &-large {
    padding: 15px;
    font-size: 1.5em;
  }

  @each $color-variant in $color-variants {
    &-#{$color-variant} {
      &.probi-button-outlined {
        border-color: map.get($colors, $color-variant);
        color: scale-color(map.get($colors, $color-variant), $lightness: -15%);

        &:hover {
          background-color: rgba(map.get($colors, $color-variant), 15%);
        }
      }
      &:not(.probi-button-outlined) {
        background-color: map.get($colors, $color-variant);
        color: $white;

        &:hover {
          background-color: scale-color(map.get($colors, $color-variant), $lightness: +15%);
        }
      }
    }
  }
}
</style>
