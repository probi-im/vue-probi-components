<template>
  <div id="app">
    <section>
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
    <section>
      <ProbiCard :outlined="true" :rounded="true" :width="0">
        <template v-slot:header>
          card header
        </template>
        <template v-slot:content>
          card content
        </template>
        <template v-slot:footer>
          card footer
        </template>
      </ProbiCard>
    </section>

    <section>
      <ProbiCardHover :title="'normal'">
        <template v-slot:text>test te</template>
      </ProbiCardHover>
      <ProbiCardHover
        :title="'small'"
        :size="'small'"
        :imgSrc="
          'https://billings.schoolspace.us/assets/facility_placeholder_square-2a7386a84e9ed7d126f124a39478556556bdc2ac4a178b05d761b4c9794cef0c.png'
        "
      ></ProbiCardHover>
      <ProbiCardHover
        :title="'largecardhover'"
        :size="'large'"
        :imgSrc="
          'https://billings.schoolspace.us/assets/facility_placeholder_square-2a7386a84e9ed7d126f124a39478556556bdc2ac4a178b05d761b4c9794cef0c.png'
        "
      >
        <template v-slot:text>this is a long text that should be wrapped</template>
      </ProbiCardHover>
    </section>
    <section>
      <ProbiInput placeholder="test" />
      <ProbiInput raised />
      <ProbiInput :rounded="false" />
      <ProbiInput raised :rounded="false" />
      <ProbiInput :rounded="false" :size="'small'" />
      <ProbiInput raised :size="'large'" />
    </section>
  </div>
</template>

<script>
import ProbiButton from './components/Button.vue';
import ProbiCard from './components/Card.vue';
import ProbiCardHover from './components/CardHover.vue';
import ProbiInput from './components/Input.vue';

export default {
  name: 'App',
  components: {
    ProbiButton,
    ProbiCard,
    ProbiCardHover,
    ProbiInput
  }
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
}
button,
input,
.probi-card,
.probi-card-hover {
  margin: 10px;
}
</style>
