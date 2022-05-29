<template>
  <router-view class="app" />
</template>

<style lang="scss" scoped>
@import 'normalize.css';

html {
}

body {
  box-sizing: border-box;

  * {
    box-sizing: inherit;
  }
}

.app {
  height: calc(100vh - 160px);
}
</style>
