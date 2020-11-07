<template>
  <input
    class="probi-input "
    :class="[
      raised ? 'probi-input-raised' : '',
      rounded ? 'probi-input-rounded' : '',
      size ? 'probi-input-' + size : ''
    ]"
  />
</template>

<script>
export default {
  name: 'ProbiInput',
  props: {
    raised: {
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

.probi-input {
  outline: none;
  border: 1px solid lightgray;
  padding: 10px;
  @include default-transition();
  font-size: 1em;

  &:focus:not(.probi-input-raised) {
    border-color: darkgray;
  }

  &-raised {
    box-shadow: 0 0 10px lightgray;

    &:focus {
      box-shadow: 0 0 10px darkgray;
    }
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
    font-size: 1.2em;
  }
}
</style>
