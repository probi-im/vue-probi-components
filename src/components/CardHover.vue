<template>
  <div class="probi-card-hover" :class="[size ? 'probi-card-hover-' + size : '']">
    <div class="probi-card-hover__title" :class="textPresent ? '' : 'no-text'">{{ title }}</div>
    <div v-if="imgSrc" class="probi-card-hover__image" :class="textPresent ? '' : 'no-text'">
      <img :src="imgSrc" />
    </div>
    <div v-if="$slots.text" class="probi-card-hover__text">
      <slot name="text"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProbiCardHover',
  props: {
    imgSrc: {
      type: String,
      default: ''
    },
    title: {
      type: String,
      default: ''
    },
    size: {
      type: String,
      default: '',
      validate: v => ['small', 'large'].includes(v)
    }
  },
  computed: {
    textPresent() {
      return this.$slots.text !== undefined;
    }
  }
};
</script>

<style lang="scss">
.probi-card-hover {
  display: flex;
  align-items: flex-end;
  min-height: 70px;
  min-width: 70px;
  width: 70px;
  border: 1px solid lightgray;
  border-radius: 15px;
  padding: 10px;
  position: relative;
  overflow: hidden;

  &:hover {
    cursor: pointer;
    .probi-card-hover__title:not(.no-text) {
      opacity: 0;
    }
    .probi-card-hover__image:not(.no-text) {
      filter: blur(2px);
    }
    .probi-card-hover__text:not(:empty) {
      transform: translateY(0%);
      opacity: 1;
    }
  }

  &__title {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    opacity: 1;
    transition: 0.3s all ease;
  }
  &__image {
    position: absolute;
    top: 0;
    left: 0;
    z-index: -10;
    filter: blur(0%);
    transition: 0.3s all ease;
    img {
      height: 100%;
      width: 100%;
    }
  }
  &__text {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    padding: 10px;
    transform: translateY(100%);
    opacity: 0;
    transition: 0.3s all ease;
    display: grid;
    place-content: center;
    &:empty {
      display: none;
    }
  }
  &-small {
    min-height: 40px;
    min-width: 40px;
    width: 40px;
    border-radius: 10px;
  }
  &-large {
    min-height: 100px;
    min-width: 100px;
    width: 100px;
    border-radius: 20px;
  }
}
</style>
