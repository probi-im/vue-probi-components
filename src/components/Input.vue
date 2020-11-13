<template>
  <div
    class="probi-input"
    :class="[
      inputFocused ? 'focused' : '',
      rounded ? 'probi-input-rounded' : '',
      size ? 'probi-input-' + size : ''
    ]"
  >
    <span v-if="$slots.prependIcon" class="input-icon"><slot name="prependIcon"></slot></span>
    <input :placeholder="placeholder" @focus="inputFocused = true" @blur="inputFocused = false" />
    <span v-if="$slots.appendIcon" class="input-icon">
      <slot name="appendIcon"></slot>
    </span>
  </div>
</template>

<script>
export default {
  name: 'ProbiInput',
  props: {
    rounded: {
      type: Boolean,
      default: true
    },
    size: {
      type: String,
      default: '',
      validate: v => ['small', 'large'].includes(v)
    },
    placeholder: {
      type: String,
      default: 'Enter text here...'
    }
  },
  data: () => ({ inputFocused: false })
};
</script>

<style lang="scss">
@import '@/assets/scss/transitions';
$input-height: 40px;
$base-color: #9898b5;
$hover-color: #757e8f;
$focus-color: #5a6375;

$border-base-color: #e4e6ea;
$border-focus-color: #2d8eff;
$border-hover-color: rgba($border-focus-color, 0.4);

.probi-input {
  @include default-transition();
  background-color: #f5f6f8;
  border: 2px solid $border-base-color;
  display: flex;
  align-items: center;
  min-height: $input-height;
  height: $input-height;
  padding: 0 7px;

  .input-icon {
    display: flex;
    flex-direction: column;
    justify-content: center;
    background-color: transparent;
    color: $base-color;
    @include default-transition();
  }

  input {
    height: 100%;
    margin-top: 1px;
    border: none;
    font-size: 1em;
    outline: none;
    background-color: transparent;
    color: $base-color;
    @include default-transition();

    &::placeholder {
      color: $base-color;
    }
    &:not(:first-child) {
      padding-left: 7px;
    }
    &:not(:last-child) {
      padding-right: 7px;
    }
  }
  &:hover {
    border-color: $border-hover-color;
    .input-icon {
      color: $hover-color;
    }

    input {
      color: $hover-color;

      &::placeholder {
        color: $hover-color;
      }
    }
  }

  &.focused {
    border-color: $border-focus-color;
    box-shadow: 0 0 0 2px $border-hover-color;
    background-color: white;

    .input-icon {
      color: $focus-color;
    }

    input {
      color: $focus-color;

      &::placeholder {
        color: $focus-color;
      }
    }
  }

  &-rounded {
    border-radius: 10px;
  }

  &-small {
    min-height: $input-height - 10px;
    height: $input-height - 10px;
    input {
      font-size: 0.8em;
      &:not(:first-child) {
        padding-left: 5px;
      }
      &:not(:last-child) {
        padding-right: 5px;
      }
    }
  }
  &-large {
    min-height: $input-height + 10px;
    height: $input-height + 10px;
    input {
      font-size: 1.2em;
      &:not(:first-child) {
        padding-left: 10px;
      }
      &:not(:last-child) {
        padding-right: 10px;
      }
    }
  }
}
</style>
