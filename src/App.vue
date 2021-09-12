<template>
  <div id="app">
    <section>
      <ProbiButton :color="'primary'">Primary button</ProbiButton>
    </section>
    <!-- <section>
      <ProbiCard :outlined="true" :rounded="true" :width="0">
        <template v-slot:header> card header </template>
        <template v-slot:content> card content </template>
        <template v-slot:footer> card footer </template>
      </ProbiCard>
    </section> -->

    <!-- <section>
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
    </section> -->
    <section>
      <ProbiInput v-model="inputText"></ProbiInput>
      Text : {{ inputText }}
    </section>
    <section>
      <ProbiToggle v-model="toggled" />
      Toggle : {{ toggled }}
    </section>
    <section>
      <ProbiLoader />
    </section>
    <!-- <section>
      <ProbiSlider :size="'small'" :fillColor="'pink'" :backgroundColor="'yellow'" />
      <ProbiSlider :lazy="false" :value.sync="sliderValue" />
      <ProbiSlider :size="'large'" :fillColor="'red'" />
    </section> -->
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
      inputText: "",
      toggled: false,
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
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  background-color: #333;
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 10px;
  height: 100vh;
}
section {
  padding: 10px;
  border: 1px solid gray;
  border-radius: 20px;
  display: flex;
  align-items: center;
  flex-wrap: wrap;
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
