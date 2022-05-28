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
@font-face {
  font-family: 'heyy-icons';
  src: url('../assets/fonts/heyy-icons.ttf') format('truetype'),
    url('../assets/fonts/heyy-icons.woff') format('woff'),
    url('../assets/fonts/heyy-icons.svg#heyy-icons') format('svg');
  font-weight: normal;
  font-style: normal;
  font-display: block;
}

/*
* Snow theme
*/
@import 'quill/dist/quill.snow.css';

/*
* Heyy theme
*/

@mixin heyyIcon {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  font-family: 'heyy-icons' !important;
  font-size: 24px;
  speak: never;
  font-style: normal;
  font-weight: normal;
  font-variant: normal;
  text-transform: none;
  line-height: 1;
  color: #404040;
  background-color: #dfdfdf;
  width: 40px;
  height: 40px;
  border-radius: 2px;
  margin: 0 1px;
  border: 1px solid #bfbfbf;

  /* Better Font Rendering =========== */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

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

    .ql-formats {
      margin-right: 0;
    }
  }
}

.ql-snow.ql-toolbar {
  .ql-color {
    @include heyyIcon;

    .ql-picker-label {
      @include heyyIcon;
      border: none;
      background-color: transparent;

      svg {
        display: none;
      }

      &::before {
        content: '\e908';
      }
    }
  }

  .ql-background {
    @include heyyIcon;

    .ql-picker-label {
      @include heyyIcon;
      border: none;
      background-color: transparent;

      svg {
        display: none;
      }

      &::before {
        content: '\e904';
      }
    }
  }
}

.ql-snow.ql-toolbar button {
  @include heyyIcon;

  svg {
    display: none;
  }

  &.ql-bold {
    &::before {
      content: '\e905';
    }
  }

  &.ql-italic {
    &::before {
      content: '\e912';
    }
  }

  &.ql-underline {
    &::before {
      content: '\e91e';
    }
  }

  &.ql-strike {
    &::before {
      content: '\e91b';
    }
  }

  &.ql-strike {
    &::before {
      content: '\e91b';
    }
  }
}
</style>
