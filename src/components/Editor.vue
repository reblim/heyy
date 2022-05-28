<template>
  <div class="editor"></div>
</template>

<script>
import Quill from 'quill';

export default {
  name: 'Editor-C',

  mounted() {
    this.init();
  },

  methods: {
    init() {
      const options = {
        // debug: 'info',
        // readOnly: true,
        // modules: {
        //   toolbar: '#toolbar',
        // },
        placeholder: 'Compose an epic...',
        theme: 'snow',
      };

      return new Quill(this.$el, options);
    },
  },
};
</script>

<style lang="scss">
.ql-container {
  &.ql-snow {
    border: none;
  }
}

.ql-editor {
  position: relative;
  max-width: 838px;
  margin: 0 auto;
  border: 2px solid red;

  &.ql-blank {
    &::before {
      right: 16px;
    }
  }
}
</style>
