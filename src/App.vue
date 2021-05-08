<template>
  <div id="app">
    <section class="hide">
      <ProbiButton :color="'primary'">Primary button</ProbiButton>
      <ProbiButton :color="'primary'" outlined>Outlined primary button</ProbiButton>
      <ProbiButton :color="'secondary'" :rounded="false">Square secondary button</ProbiButton>
      <ProbiButton :color="'secondary'" outlined>Outlined secondary button</ProbiButton>
      <ProbiButton :color="'accent'">Accent button</ProbiButton>
      <ProbiButton :color="'accent'" outlined :rounded="false">
        Outlined square accent button
      </ProbiButton>
      <ProbiButton :color="'primary'" :size="'small'">Small primary button</ProbiButton>
      <ProbiButton :color="'primary'" outlined>Primary button</ProbiButton>
      <ProbiButton :color="'primary'" :rounded="false" :size="'large'">
        Large primary button
      </ProbiButton>
    </section>
    <section class="hide">
      <ProbiCard :outlined="true" :rounded="true" :width="0">
        <template v-slot:header> card header </template>
        <template v-slot:content> card content </template>
        <template v-slot:footer> card footer </template>
      </ProbiCard>
    </section>

    <section class="hide">
      <ProbiCardHover :title="'normal'">
        <template v-slot:text>test te</template>
      </ProbiCardHover>
      <ProbiCardHover
        :title="'small'"
        :size="'small'"
        :imgSrc="'https://billings.schoolspace.us/assets/facility_placeholder_square-2a7386a84e9ed7d126f124a39478556556bdc2ac4a178b05d761b4c9794cef0c.png'"
      ></ProbiCardHover>
      <ProbiCardHover
        :title="'largecardhover'"
        :size="'large'"
        :imgSrc="'https://billings.schoolspace.us/assets/facility_placeholder_square-2a7386a84e9ed7d126f124a39478556556bdc2ac4a178b05d761b4c9794cef0c.png'"
      >
        <template v-slot:text>this is a long text that should be wrapped</template>
      </ProbiCardHover>
    </section>
    <section v-for="color in ['light', 'dark']" :key="color" :class="[color, 'hide']">
      <ProbiInput></ProbiInput>
      <ProbiInput disabled></ProbiInput>
      <ProbiInput :rounded="false"> </ProbiInput>
      <ProbiInput :size="'small'"> </ProbiInput>
      <ProbiInput :size="'large'"> </ProbiInput>
      <ProbiInput>
        <template v-slot:prependIcon><i class="material-icons">face</i></template>
      </ProbiInput>
      <ProbiInput>
        <template v-slot:appendIcon><i class="material-icons">stop</i></template>
      </ProbiInput>
      <ProbiInput>
        <template v-slot:prependIcon><i class="material-icons">face</i></template>
        <template v-slot:appendIcon><i class="material-icons">stop</i></template>
      </ProbiInput>
      <ProbiButton></ProbiButton>
      <ProbiButton disabled>Disabled button</ProbiButton>
      <ProbiButton :rounded="false">Square button</ProbiButton>
      <ProbiButton :rounded="false" disabled>Disabled square button</ProbiButton>
      <ProbiButton :size="'small'">Small button</ProbiButton>
      <ProbiButton :size="'large'">Large button</ProbiButton>
    </section>
    <section class="light hide">
      <ProbiToggle :value="true" :size="'x-small'" />
      <ProbiToggle :value="false" :size="'small'" :rounded="false" />
      <ProbiToggle :value="true" :outlined="true" />
      <ProbiToggle :value="false" :size="'large'" />
      <ProbiToggle :value="true" :size="'x-large'" :rounded="false" />
    </section>
    <section class="light hide">
      <ProbiLoader :width="20" />
      <ProbiLoader />
      <ProbiLoader :width="50" />
      <ProbiLoader :strokeWidth="4" />
    </section>
    <section class="light">
      <ProbiSlider :size="'small'" :fillColor="'pink'" :backgroundColor="'yellow'" />
      <ProbiSlider :lazy="false" :value.sync="sliderValue" />
      <ProbiSlider :size="'large'" :fillColor="'red'" />
    </section>
  </div>
</template>

<script>
import ProbiButton from './components/Button.vue';
import ProbiCard from './components/Card.vue';
import ProbiCardHover from './components/CardHover.vue';
import ProbiInput from './components/Input.vue';
import ProbiToggle from './components/Toggle.vue';
import ProbiLoader from './components/Loader.vue';
import ProbiSlider from './components/Slider.vue';

export default {
  name: 'App',
  components: {
    ProbiButton,
    ProbiCard,
    ProbiCardHover,
    ProbiInput,
    ProbiToggle,
    ProbiLoader,
    ProbiSlider,
  },
  data() {
    return {
      sliderValue: 20,
      sliderInterval: null,
    };
  },
  methods: {
    testSliders(v) {
      // console.log(v);
    },
  },
  mounted() {
    this.sliderInterval = setInterval(() => {
      if (this.sliderValue + 5 <= 100) this.sliderValue += 5;
      else this.sliderValue = 0;
    }, 1000);
  },
  destroyed() {
    if (this.sliderInterval) clearInterval(this.sliderInterval);
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
section {
  margin: 10px;
  padding: 10px;
  border: 1px solid gray;
  border-radius: 20px;
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  &.light {
    background-color: #fefefe;
  }
  &.dark {
    background-color: #333;
  }
}
.probi-button,
.probi-input,
.probi-card,
.probi-card-hover,
.probi-toggle,
.probi-loader,
.probi-slider {
  margin: 10px;
}
.hide {
  display: none;
}
</style>
