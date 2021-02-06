<template>
  <div class="wysiwyg">
    <div class="controls">
      <Button @click="undo">
        <svg>
          <use xlink:href="@/assets/sprite.svg#go-back-arrow"/>
        </svg>
      </Button>
      <Button @click="redo">
        <svg class="rotate-180">
          <use xlink:href="@/assets/sprite.svg#go-back-arrow"/>
        </svg>
      </Button>
      <Button @click="heading">
        <svg>
          <use xlink:href="@/assets/sprite.svg#t-icon"/>
        </svg>
      </Button>
      <Button @click="paragraph">
        <svg>
          <use xlink:href="@/assets/sprite.svg#paragraph"/>
        </svg>
      </Button>
      <Button @click="addImage">
        <svg>
          <use xlink:href="@/assets/sprite.svg#image"/>
        </svg>
      </Button>
      <Button @click="copyHtml">
        Скопировать HTML
      </Button>
    </div>
    <div contenteditable class="editor" ref="editor">efewfe</div>
  </div>
</template>

<script>
import Button from "@/components/Button";

export default {
  name: "Wysiwig",
  components: {
    Button
  },
  methods: {
    heading() {
      console.log('heading')
      document.execCommand('formatBlock', false, 'h1');
    },
    paragraph() {
      console.log('p')
      document.execCommand('formatBlock', false, 'p');
    },
    copyHtml() {
      const html = this.$refs.editor.innerHTML;
      navigator.clipboard.writeText(html);
      alert(html);
      console.log(html);
    },
    insertImage() {

    },
    undo() {
      document.execCommand('undo', false, '')
    },
    redo() {
      document.execCommand('redo', false, '')
    },
    addImage() {
      console.log('image')
      const src = prompt('Введите URL изображения', '');
      if (!src) {
        alert('URL пустой')
      } else {
        console.log('url', src);
        document.execCommand('insertImage', false, src);
      }
    },
    clear() {
      document.execCommand('clear');
    }
  }
}
</script>

<style scoped>

.controls {
  display: grid;
  grid-template-columns: repeat(6, auto);
  justify-content: start;
  align-content: center;
  grid-gap: 24px;
}

.editor {
  margin-top: 40px;
  min-height: 500px;
  max-height: 500px;
  overflow: auto;
  box-shadow: 0 0 0 2px var(--action-element-color);
  border-right: 4px;
  padding: 12px;
}

.editor:focus {
  box-shadow: none;
}

.rotate-180 {
  transform: rotateY(180deg);
}
</style>
