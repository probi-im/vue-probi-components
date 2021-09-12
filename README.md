# Vue Probi Components

Simple Vue components made for my own usage. Currently only support Vue 2.

## Installation

```
npm install vue-probi-components
```

## Usage

Inside a Vue SFC :

```vue
<template>
  <div class="test">
    <ProbiButton>Button</ProbiButton>
    <ProbiCard :outlined="true" :rounded="true" :width="0">
      <template v-slot:header>Card header</template>
      <template v-slot:content>Card content</template>
      <template v-slot:footer>Card footer</template>
    </ProbiCard>
    <ProbiCardHover :title="'normal'">
      <template v-slot:text>Text sample</template>
    </ProbiCardHover>
    <ProbiInput v-model="text"></ProbiInput>
    <ProbiToggle v-model="toggled" />
    <ProbiLoader />
  </div>
</template>

<script>
import {
  ProbiButton,
  ProbiCard,
  ProbiCardHover,
  ProbiInput,
  ProbiToggle,
  ProbiLoader
} from "vue-probi-components";

export default {
  ...
  components: {
    ...
    ProbiButton,
    ProbiCard,
    ProbiCardHover,
    ProbiInput,
    ProbiToggle,
    ProbiLoader
  },
  ...
}
</script>
```

## "v-model" support

Components that are compatible with the "v-model" directive :
- ProbiInput
- ProbiToggle
