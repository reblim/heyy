<template>
  <router-view class="app" />
</template>

<style lang="scss" scoped>
@import 'normalize.css';
@import url('https://fonts.googleapis.com/css2?family=Source+Code+Pro:wght@400;600&family=Source+Sans+Pro:wght@400;600&family=Source+Serif+Pro:wght@400;600&display=swap');

html {
}

body {
  box-sizing: border-box;
  font-family: 'Source Sans Pro', sans-serif;

  * {
    box-sizing: inherit;
  }
}

.app {
  height: calc(100vh - 160px);
}
</style>
