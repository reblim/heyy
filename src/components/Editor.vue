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
            { size: ['small', false] },
            { header: [1, 2, 3, 4, 5, 6] },
            'bold',
            'italic',
            'underline',
            'strike',
            'mark',
            { color: ['#404040', '#303030', '#202020', '#101010', '#000000'] },
            {
              background: [
                '#bfbfbf',
                '#cfcfcf',
                '#dfdfdf',
                '#efefef',
                '#ffffff',
              ],
            },
            { script: 'sub' },
            { script: 'super' },
            'blockquote',
            'code-block',
            { list: 'ordered' },
            { list: 'bullet' },
            { indent: '-1' },
            { indent: '+1' },
            { align: [] },
            { direction: 'rtl' },
            'link',
            'image',
            'video',
            'clean',
          ],
        },
        placeholder: 'Start writing...',
        theme: 'snow',
      };

      const Inline = Quill.import('blots/inline');

      class MarkedText extends Inline {
        static create() {
          return super.create();
        }
      }

      MarkedText.blotName = 'mark';
      MarkedText.tagName = 'mark';
      Quill.register(MarkedText);

      const editor = new Quill(this.$el, options);

      setTimeout(() => {
        const spanBlockButton = document.querySelector('.ql-mark');
        spanBlockButton.addEventListener('click', () => {
          const range = editor.getSelection();
          if (range) editor.formatText(range, 'mark');
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
  color: var(--color-contrast-lowest);
  background-color: var(--color-background-tertiary);
  width: var(--size-100);
  height: var(--size-100);
  border-radius: var(--size-20);
  margin: 0 var(--size-20);
  border: var(--size-10) solid var(--color-disabled);

  &:hover {
    background-color: var(--color-background-secondary);
    color: var(--color-contrast-lowest);
    border-color: var(--color-contrast-highest);
  }

  &.ql-active {
    background-color: var(--color-background-primary);
    color: var(--color-contrast-lowest);
    border-color: var(--color-contrast-lowest);
  }
}

@mixin heyyIcon {
  @include heyyIconButton;
  font-family: 'heyy-icons' !important;
  font-size: var(--font-size-icon);
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
  display: inline-flex;
  justify-content: space-evenly;
  align-items: center;
  padding: var(--size-20);
  border-radius: var(--size-20);
  margin-bottom: var(--size-30);
  top: initial;
  bottom: 100%;
  left: 0;
  right: initial;
  width: initial;
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
  max-width: 728px;
  margin: 40px auto 0;
  padding: 40px;
  // border-left: var(--size-10) solid var(--color-background-secondary);
  // border-right: var(--size-10) solid var(--color-background-secondary);
  caret-color: var(--color-contrast-lowest);
  font-family: 'Source Sans Pro', sans-serif;

  &.ql-blank {
    &::before {
      left: 40px;
      color: var(--color-disabled);
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

  .ql-size-small {
    font-size: var(--font-size-text-small);
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
  background-color: var(--color-background-tertiary);
  color: var(--color-contrast-lowest);
  padding: var(--size-30) 8px;
  border-radius: var(--size-30);
  font-size: var(--font-size-text-small);
}

.ql-snow .ql-picker.ql-expanded {
  .ql-picker-options {
    @include optionsDropdown;
  }
}

.ql-snow.ql-toolbar {
  .ql-mark {
    &:before {
      content: '\e923';
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

  .ql-size {
    @include heyyIcon;

    .ql-picker-label {
      @include heyyIcon;
      border: none;
      background-color: transparent;

      &:hover {
        border: none;
        background-color: transparent;
      }

      &:before {
        content: '\e922';
      }

      &[data-value='small'] {
        border: none;
        background-color: transparent;
        &:before {
          font-size: var(--font-size-text-small);
          content: '\e922';
        }
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
          font-size: var(--font-size-icon);
          content: '\e900';
        }
      }

      &[data-value='right'] {
        border: none;
        background-color: transparent;
        &:before {
          font-size: var(--font-size-icon);
          content: '\e903';
        }
      }

      &[data-value='justify'] {
        border: none;
        background-color: transparent;
        &:before {
          font-size: var(--font-size-icon);
          content: '\e901';
        }
      }
    }
  }

  .ql-header {
    .ql-picker-item {
      @include heyyIcon;

      &:first-of-type {
        margin-left: 0;
      }

      &:last-of-type {
        margin-right: 0;
      }

      &[data-value='1'] {
        &:before {
          font-size: var(--font-size-icon);
          content: '\e90a';
        }
      }

      &[data-value='2'] {
        &:before {
          font-size: var(--font-size-icon);
          content: '\e90b';
        }
      }

      &[data-value='3'] {
        &:before {
          font-size: var(--font-size-icon);
          content: '\e90c';
        }
      }

      &[data-value='4'] {
        &:before {
          font-size: var(--font-size-icon);
          content: '\e90d';
        }
      }

      &[data-value='5'] {
        &:before {
          font-size: var(--font-size-icon);
          content: '\e90e';
        }
      }

      &[data-value='6'] {
        &:before {
          font-size: var(--font-size-icon);
          content: '\e90f';
        }
      }
    }
  }

  .ql-size {
    .ql-picker-item {
      @include heyyIcon;

      &:first-of-type {
        margin-left: 0;
      }

      &:last-of-type {
        margin-right: 0;
      }

      &:before {
        content: '\e922';
      }

      &[data-value='small'] {
        &:before {
          content: '\e922';
          font-size: var(--font-size-text-small);
        }
      }
    }
  }

  .ql-align {
    .ql-picker-item {
      @include heyyIcon;

      &:first-of-type {
        margin-left: 0;
      }

      &:last-of-type {
        margin-right: 0;
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

.ql-snow .ql-color-picker.ql-color .ql-picker-item,
.ql-snow .ql-color-picker.ql-background .ql-picker-item {
  @include heyyIcon;
  border-radius: 100%;

  &:first-of-type {
    margin-left: 0;
  }

  &:last-of-type {
    margin-right: 0;
  }
}

.ql-toolbar.ql-snow .ql-size.ql-picker.ql-expanded .ql-picker-options,
.ql-toolbar.ql-snow .ql-color.ql-picker.ql-expanded .ql-picker-options,
.ql-toolbar.ql-snow .ql-background.ql-picker.ql-expanded .ql-picker-options,
.ql-toolbar.ql-snow .ql-align.ql-picker.ql-expanded .ql-picker-options {
  left: -1px;
}

.ql-toolbar.ql-snow .ql-header.ql-picker.ql-expanded .ql-picker-options {
  left: 1px;
}

.ql-snow.ql-toolbar .ql-color .ql-picker-label.ql-active,
.ql-snow.ql-toolbar .ql-background .ql-picker-label.ql-active {
  width: calc(100% - var(--size-10));
  height: calc(100% - var(--size-10));
}

.ql-snow .ql-picker-options {
  background-color: var(--color-background-primary);
}

.ql-toolbar.ql-snow .ql-picker-options {
  box-shadow: none;
}

.ql-toolbar.ql-snow .ql-picker.ql-expanded .ql-picker-options {
  border: var(--size-10) solid var(--color-disabled);
}

.ql-snow .ql-tooltip {
  border-radius: 2px;
  padding: 4px;
}

.ql-snow .ql-tooltip.ql-flip {
  transform: translateY(0);
}

.ql-snow .ql-tooltip a.ql-action::after {
}

.ql-snow .ql-picker.ql-expanded.ql-font .ql-picker-options {
  flex-direction: column;
}

.ql-snow .ql-tooltip.ql-editing input[type='text'] {
  display: inline-flex;
}

.ql-snow .ql-picker-label::before {
  line-height: 1;
}

.ql-snow .ql-tooltip.ql-editing a.ql-action::after {
  @include heyyIcon;
  content: '\e924';
  margin: 0;
}

.ql-snow {
  .ql-picker {
    font-size: var(--font-size-icon);

    height: auto;
  }

  .ql-picker-label {
    padding: 0;
  }

  .ql-picker.ql-header {
    width: auto;

    .ql-picker-label {
      @include heyyIcon;
      font-size: var(--font-size-icon-large);

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
