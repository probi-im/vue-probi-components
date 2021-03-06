<template>
  <div
    class="probi-input"
    :class="[
      disabled ? 'disabled' : '',
      inputFocused ? 'focused' : '',
      rounded ? 'probi-input-rounded' : '',
      size ? 'probi-input-' + size : ''
    ]"
  >
    <span v-if="$slots.prependIcon" class="input-icon"><slot name="prependIcon"></slot></span>
    <input
      v-model="inputValue"
      :disabled="disabled"
      :placeholder="placeholder"
      @focus="inputFocused = true"
      @blur="inputFocused = false"
    />
    <span v-if="$slots.appendIcon" class="input-icon">
      <slot name="appendIcon"></slot>
    </span>
  </div>
</template>

<script>
export default {
  name: 'ProbiInput',
  props: {
    disabled: {
      type: Boolean,
      default: false
    },
    placeholder: {
      type: String,
      default: 'Enter text here...'
    },
    rounded: {
      type: Boolean,
      default: true
    },
    size: {
      type: String,
      default: '',
      validate: v => ['small', 'large'].includes(v)
    },
    value: {
      type: String,
      default: ''
    }
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
  },
  data: () => ({ inputFocused: false })
};
</script>

<style lang="scss">
@import '@/assets/scss/transitions';
@import '@/assets/scss/variables';

.probi-input {
  @include default-transition();
  background-color: $background-secondary-color;
  border: 2px solid $border-base-color;
  display: flex;
  align-items: center;
  min-height: $element-height;
  height: $element-height;
  padding: 0 7px;

  .input-icon {
    display: flex;
    flex-direction: column;
    justify-content: center;
    background-color: transparent;
    color: $text-secondary-color;
    @include default-transition();
  }

  input {
    height: 100%;
    margin-top: 1px;
    border: none;
    font-size: 1em;
    outline: none;
    background-color: transparent;
    color: $text-secondary-color;
    @include default-transition();

    &::placeholder {
      color: $text-secondary-color;
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
      color: $text-base-color;
    }

    input {
      color: $text-base-color;

      &::placeholder {
        color: $text-base-color;
      }
    }
  }

  &.disabled {
    border-color: $border-disabled-color;

    .input-icon {
      color: $text-disabled-color;
      cursor: default;
    }

    input {
      color: $text-disabled-color;

      &::placeholder {
        color: $text-disabled-color;
      }
    }
  }

  &.focused {
    border-color: $border-focus-color;
    box-shadow: 0 0 0 2px $border-hover-color;
    background-color: $background-base-color;

    .input-icon {
      color: $text-base-color;
    }

    input {
      color: $text-base-color;

      &::placeholder {
        color: $text-base-color;
      }
    }
  }

  &-rounded {
    border-radius: 10px;
  }

  &-small {
    min-height: $element-height - 10px;
    height: $element-height - 10px;
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
    min-height: $element-height + 10px;
    height: $element-height + 10px;
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
