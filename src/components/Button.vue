<template>
  <button
    :disabled="disabled"
    class="probi-button "
    :class="[rounded ? 'probi-button-rounded' : '', size ? 'probi-button-' + size : '']"
  >
    <slot></slot>
    <span v-if="!$slots.default">Button</span>
  </button>
</template>

<script>
export default {
  name: 'ProbiButton',
  props: {
    disabled: {
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
@import '@/assets/scss/transitions';
@import '@/assets/scss/variables';

.probi-button {
  @include default-transition();
  outline: none;
  background-color: $background-base-color;
  border: 2px solid $border-base-color;
  border-radius: 0px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 10px;
  font-size: 1.1em;
  min-width: 30px;
  min-height: $element-height;
  color: $text-base-color;

  &:hover:not(:disabled) {
    cursor: pointer;
    border-color: $border-hover-color;
  }
  &:active:not(:disabled) {
    box-shadow: 0 0 0 2px $border-hover-color;
  }
  &:active:not(:disabled),
  &:focus:not(:disabled) {
    border-color: $border-focus-color;
  }
  &:disabled {
    color: $text-disabled-color;
    border-color: $border-disabled-color;
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
    min-height: $element-height - 10px;
    height: $element-height - 10px;
    padding: 8px;
    font-size: 0.8em;
  }
  &-large {
    min-height: $element-height + 10px;
    height: $element-height + 10px;
    padding: 12px;
    font-size: 1.5em;
  }
}
</style>
