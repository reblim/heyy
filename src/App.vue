<template>
  <router-view class="app" />
</template>

<script>
export default {
  name: 'App',

  mounted() {
    // document.querySelector('html').classList.add('dark');
  },
};
</script>

<style lang="scss">
@import 'normalize.css';
@import url('https://fonts.googleapis.com/css2?family=Source+Code+Pro:wght@400;600&family=Source+Sans+Pro:wght@400;600&family=Source+Serif+Pro:wght@400;600&display=swap');

html {
  background-color: var(--color-background-primary);
  color: var(--color-contrast-lowest);
}

body {
  box-sizing: border-box;
  font-family: 'Source Sans Pro', sans-serif;

  * {
    box-sizing: inherit;
  }

  ::selection {
    background-color: var(--color-background-tertiary);
  }
}

.app {
  height: calc(100vh - 160px);
}
</style>
