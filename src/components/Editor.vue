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
            { font: [] },
            'small',
            { header: [1, 2, 3, 4, 5, 6, false] },
            'bold',
            'italic',
            'underline',
            'strike',
            { color: [] },
            { background: [] },
            { script: 'sub' },
            { script: 'super' },
            'blockquote',
            'code-block',
            { list: 'ordered' },
            { list: 'bullet' },
            { indent: '-1' },
            { indent: '+1' },
            { align: [] },
            'link',
            'image',
            'video',
            { direction: 'rtl' },
            'clean',
          ],
        },
        placeholder: 'Start writing...',
        theme: 'snow',
      };

      const Inline = Quill.import('blots/inline');

      class SmallText extends Inline {
        static create() {
          return super.create();
        }
      }

      SmallText.blotName = 'small';
      SmallText.tagName = 'small';
      Quill.register(SmallText);

      const editor = new Quill(this.$el, options);

      setTimeout(() => {
        const spanBlockButton = document.querySelector('.ql-small');
        spanBlockButton.addEventListener('click', () => {
          const range = editor.getSelection();
          if (range) editor.formatText(range, 'small');
        });
      });

      return editor.focus();
    },
  },
};
</script>

<style lang="scss">
@import '../scss/mixins';

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
  width: 32px;
  height: 32px;
  border-radius: 2px;
  margin: 0 1px;
  border: 1px solid #bfbfbf;

  &:hover {
    background-color: #efefef;
    color: #404040;
  }

  &.ql-active {
    background-color: #ffffff;
    color: #404040;
    border-color: #404040;
  }
}

@mixin heyyIcon {
  @include heyyIconButton;
  font-family: 'heyy-icons' !important;
  font-size: var(--font-size-icons);
  speak: never;
  font-style: normal;
  font-weight: normal;
  font-variant: normal;
  text-transform: none;
  line-height: 1;

  /* Better Font Rendering =========== */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  svg {
    display: none;
  }
}

@mixin optionsDropdown {
  display: flex;
  flex-direction: column;
  padding: 4px;
  border-radius: 2px;
  margin-bottom: 4px;
  top: initial;
  bottom: 100%;
  left: -4px;
}

.ql-container {
  &.ql-snow {
    border: none;
  }
}

.ql-snow .ql-editor {
  @include fontSize;
}

.ql-editor {
  position: relative;
  max-width: 838px;
  margin: 40px auto 0;
  padding: 40px;
  border-left: 1px solid #efefef;
  border-right: 1px solid #efefef;
  caret-color: #404040;
  font-family: 'Source Sans Pro', sans-serif;
  line-height: 1.5;

  &.ql-blank {
    &::before {
      left: 40px;
      color: #bfbfbf;
      font-weight: normal;
      font-style: normal;
    }
  }

  .ql-font-serif {
    font-family: 'Source Serif Pro', serif;
  }

  .ql-font-monospace {
    font-family: 'Source Code Pro', monospace;
  }
}

.ql-toolbar {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 16px;

  &.ql-snow {
    border: none;
    padding: 0;
    margin: 40px 0;

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

.ql-snow .ql-picker.ql-expanded {
  .ql-picker-options {
    @include optionsDropdown;
  }
}

.ql-snow.ql-toolbar {
  .ql-small {
    &:before {
      content: '\e922';
      font-size: var(--font-size-text-small);
    }
  }

  .ql-color {
    @include heyyIcon;

    .ql-picker-label {
      @include heyyIcon;
      border: none;
      background-color: transparent;

      &:hover {
        background-color: transparent;
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

      &:hover {
        background-color: transparent;
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

      &:hover {
        border: none;
        background-color: transparent;
      }

      &::before {
        content: '\e902';
      }

      &[data-value='center'] {
        border: none;
        background-color: transparent;
        &:before {
          font-size: var(--font-size-icons);
          content: '\e900';
        }
      }

      &[data-value='right'] {
        border: none;
        background-color: transparent;
        &:before {
          font-size: var(--font-size-icons);
          content: '\e903';
        }
      }

      &[data-value='justify'] {
        border: none;
        background-color: transparent;
        &:before {
          font-size: var(--font-size-icons);
          content: '\e901';
        }
      }
    }
  }

  .ql-header {
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
          font-size: var(--font-size-icons);
          content: '\e90a';
        }
      }

      &[data-value='2'] {
        &:before {
          font-size: var(--font-size-icons);
          content: '\e90b';
        }
      }

      &[data-value='3'] {
        &:before {
          font-size: var(--font-size-icons);
          content: '\e90c';
        }
      }

      &[data-value='4'] {
        &:before {
          font-size: var(--font-size-icons);
          content: '\e90d';
        }
      }

      &[data-value='5'] {
        &:before {
          font-size: var(--font-size-icons);
          content: '\e90e';
        }
      }

      &[data-value='6'] {
        &:before {
          font-size: var(--font-size-icons);
          content: '\e90f';
        }
      }
    }
  }

  .ql-align {
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
        content: '\e902';
      }

      &[data-value='center'] {
        &:before {
          content: '\e900';
        }
      }

      &[data-value='right'] {
        &:before {
          content: '\e903';
        }
      }

      &[data-value='justify'] {
        &:before {
          content: '\e901';
        }
      }
    }
  }
}

.ql-snow .ql-picker.ql-font {
  @include heyyIconButton;
  width: 80px;
  text-align: center;
}

.ql-snow .ql-picker-label {
  svg {
    display: none !important;
  }

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
  font-family: 'Source Sans Pro', sans-serif;
}

.ql-snow .ql-picker.ql-font .ql-picker-label[data-value='serif']::before,
.ql-snow .ql-picker.ql-font .ql-picker-item[data-value='serif']::before {
  content: 'Serif';
  font-family: 'Source Serif Pro', serif;
}

.ql-snow .ql-picker.ql-font .ql-picker-label[data-value='monospace']::before,
.ql-snow .ql-picker.ql-font .ql-picker-item[data-value='monospace']::before {
  content: 'Mono';
  font-family: 'Source Code Pro', sans-serif;
}

.ql-snow {
  .ql-picker {
    font-size: var(--font-size-icons);

    height: auto;
  }

  .ql-picker-label {
    padding: 0;
  }

  .ql-picker.ql-header {
    width: auto;

    .ql-picker-label {
      @include heyyIcon;

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
