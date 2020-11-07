<template>
  <div
    class="probi-card"
    :class="[outlined ? 'probi-card-outlined' : '', rounded ? 'probi-card-rounded' : '']"
    :style="width ? 'width: ' + width + 'px;' : 'width: auto;flex: 1;'"
  >
    <div class="probi-card__header">
      <slot name="header"></slot>
    </div>
    <div class="probi-card__content">
      <slot name="content"></slot>
    </div>
    <div class="probi-card__footer">
      <slot name="footer"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProbiCard',
  props: {
    outlined: {
      type: Boolean,
      default: false
    },
    rounded: {
      type: Boolean,
      default: true
    },
    width: {
      type: Number,
      default: 0
    }
  }
};
</script>

<style lang="scss">
$card-x-padding: 20px;
$card-y-padding: 10px;
$border-color: lightgray;

.probi-card {
  box-shadow: 0 0 10px $border-color;
  display: flex;
  flex-direction: column;

  &-rounded {
    border-radius: 10px;
  }

  &-outlined {
    border: 1px solid $border-color;
    box-shadow: none;
  }

  &__header {
    padding: $card-y-padding $card-x-padding;
    font-size: 1.5em;
    border-bottom: 1px solid $border-color;
    display: flex;
    align-items: center;
  }
  &__content {
    padding: $card-y-padding $card-x-padding;
  }
  &__footer {
    padding: $card-y-padding $card-x-padding;
    border-top: 1px solid $border-color;
    display: flex;
    align-items: center;
  }
  &__header:empty,
  &__footer:empty {
    display: none;
  }
}
</style>
