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
        modules: {
          toolbar: [
            [{ font: [] }],
            [{ header: [1, 2, 3, 4, 5, 6, false] }],
            ['bold', 'italic', 'underline', 'strike'],
            [{ color: [] }, { background: [] }],
            [{ script: 'sub' }, { script: 'super' }],
            ['blockquote', 'code-block'],
            [{ list: 'ordered' }, { list: 'bullet' }],
            [{ indent: '-1' }, { indent: '+1' }, { align: [] }],
            ['link', 'image', 'video'],
            [{ direction: 'rtl' }],
            ['clean'],
          ],
        },

        placeholder: 'Start writing...',
        theme: 'snow',
      };

      return new Quill(this.$el, options);
    },
  },
};
</script>

<style lang="scss">
/*!
 * Quill Editor v1.3.7
 * https://quilljs.com/
 * Copyright (c) 2014, Jason Chen
 * Copyright (c) 2013, salesforce.com
 */
@import 'quill/dist/quill.snow.css';

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

.ql-toolbar {
  display: flex;
  justify-content: center;
  align-items: center;

  &.ql-snow {
    border: none;
  }
}
</style>
