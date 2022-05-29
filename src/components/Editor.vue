<template>
  <div class="editor"></div>
</template>

<script>
import Quill from 'quill';

export default {
  name: 'Editor-C',

  mounted() {
    return this.init();
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

      const editor = new Quill(this.$el, options);
      return editor.focus();
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

@mixin heyyIconButton {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  color: #404040;
  background-color: #dfdfdf;
  width: 40px;
  height: 40px;
  border-radius: 2px;
  margin: 0 1px;
  border: 1px solid #bfbfbf;

  &.ql-active {
    background-color: #ffffff;
    color: #404040;
    border-color: #404040;
  }
}

@mixin heyyIcon {
  @include heyyIconButton;
  font-family: 'heyy-icons' !important;
  font-size: 24px;
  speak: never;
  font-style: normal;
  font-weight: normal;
  font-variant: normal;
  text-transform: none;
  line-height: 1;

  /* Better Font Rendering =========== */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.ql-container {
  font-size: 20px;

  &.ql-snow {
    border: none;
  }
}

.ql-editor {
  position: relative;
  max-width: 838px;
  margin: 0 auto;
  border: 1px solid #bfbfbf;
  border-radius: 4px;

  &.ql-blank {
    &::before {
      color: #bfbfbf;
      font-weight: normal;
    }
  }

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
    padding: 0;
    margin: 40px 16px;

    .ql-formats {
      margin-right: 0;
    }
  }
}

.ql-snow .ql-editor pre.ql-syntax {
  background-color: #404040;
  padding: 4px 8px;
  border-radius: 4px;
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

  .ql-align {
    @include heyyIcon;

    .ql-picker-label {
      @include heyyIcon;
      border: none;
      background-color: transparent;

      svg {
        display: none;
      }

      &::before {
        content: '\e902';
      }
    }
  }

  .ql-header {
    &.ql-expanded {
      .ql-picker-options {
        display: flex;
        flex-direction: column;
        padding: 4px;
        border-radius: 2px;
        margin-top: 4px;
        left: -4px;
      }
    }

    .ql-picker-item {
      @include heyyIcon;
      margin: 1px 0;

      &:first-of-type {
        margin-top: 0;
      }

      &:last-of-type {
        margin-bottom: 0;
      }

      &:before {
        content: '\e922';
      }

      &[data-value='1'] {
        &:before {
          font-size: 24px;
          content: '\e90a';
        }
      }

      &[data-value='2'] {
        &:before {
          font-size: 24px;
          content: '\e90b';
        }
      }

      &[data-value='3'] {
        &:before {
          font-size: 24px;
          content: '\e90c';
        }
      }

      &[data-value='4'] {
        &:before {
          font-size: 24px;
          content: '\e90d';
        }
      }

      &[data-value='5'] {
        &:before {
          font-size: 24px;
          content: '\e90e';
        }
      }

      &[data-value='6'] {
        &:before {
          font-size: 24px;
          content: '\e90f';
        }
      }
    }
  }
}

.ql-snow .ql-picker.ql-font {
  @include heyyIconButton;
  width: 80px;
  text-align: center;

  svg {
    display: none;
  }
}

.ql-snow .ql-picker-label {
  &::before {
    display: inline-flex;
    justify-content: center;
    align-items: center;
    height: inherit;
  }
}

.ql-snow .ql-picker.ql-font .ql-picker-label::before,
.ql-snow .ql-picker.ql-font .ql-picker-item::before {
  content: 'Sans';
  font-family: sans-serif;
}

.ql-snow .ql-picker.ql-font .ql-picker-label[data-value='serif']::before,
.ql-snow .ql-picker.ql-font .ql-picker-item[data-value='serif']::before {
  content: 'Serif';
  font-family: serif;
}

.ql-snow .ql-picker.ql-font .ql-picker-label[data-value='monospace']::before,
.ql-snow .ql-picker.ql-font .ql-picker-item[data-value='monospace']::before {
  content: 'Mono';
  font-family: monospace;
}

.ql-snow {
  .ql-picker {
    font-size: 24px;
    height: auto;
  }

  .ql-picker-label {
    padding: 0;
  }

  .ql-picker.ql-header {
    width: auto;

    .ql-picker-label {
      @include heyyIcon;

      svg {
        display: none;
      }

      &::before {
        content: '\e922';
      }

      &[data-value='1'] {
        &:before {
          content: '\e90a';
        }
      }

      &[data-value='2'] {
        &:before {
          content: '\e90b';
        }
      }

      &[data-value='3'] {
        &:before {
          content: '\e90c';
        }
      }

      &[data-value='4'] {
        &:before {
          content: '\e90d';
        }
      }

      &[data-value='5'] {
        &:before {
          content: '\e90e';
        }
      }

      &[data-value='6'] {
        &:before {
          content: '\e90f';
        }
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

  &.ql-script {
    &[value='sub'] {
      &::before {
        content: '\e91c';
      }
    }

    &[value='super'] {
      &::before {
        content: '\e91d';
      }
    }
  }

  &.ql-blockquote {
    &::before {
      content: '\e919';
    }
  }

  &.ql-code-block {
    &::before {
      content: '\e907';
    }
  }

  &.ql-list {
    &[value='ordered'] {
      &::before {
        content: '\e914';
      }
    }

    &[value='bullet'] {
      &::before {
        content: '\e915';
      }
    }
  }

  &.ql-indent {
    &[value='+1'] {
      &::before {
        content: '\e911';
      }
    }

    &[value='-1'] {
      &::before {
        content: '\e918';
      }
    }
  }

  &.ql-link {
    &::before {
      content: '\e913';
    }
  }

  &.ql-image {
    &::before {
      content: '\e910';
    }
  }

  &.ql-video {
    &::before {
      content: '\e91f';
    }
  }

  &.ql-direction {
    &[value='rtl'] {
      svg {
        display: none;
      }

      &::before {
        content: '\e91a';
      }
    }
  }

  &.ql-clean {
    &::before {
      content: '\e906';
    }
  }
}
</style>
