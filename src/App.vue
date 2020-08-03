<template>
  <div id="app">
    <app-emoji></app-emoji>
  </div>
</template>

<script>
import Emoji from './components/Emoji';

export default {
  data() {
    return {};
  },
  components: {
    appEmoji: Emoji
  }
};
</script>

<style lang="scss">
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

*,
*::after,
::before {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

html {
  font-size: 62.5%;
  box-sizing: border-box;
}

body {
  font-family: 'Mulish', sans-serif;
  font-size: 1.6rem;
}
</style>
