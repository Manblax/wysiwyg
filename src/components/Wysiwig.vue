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
      <Button @click="tag" data-tag="h1">
        <svg>
          <use xlink:href="@/assets/sprite.svg#t-icon"/>
        </svg>
      </Button>
      <Button @click="tag" data-tag="p">
        <svg>
          <use xlink:href="@/assets/sprite.svg#paragraph"/>
        </svg>
      </Button>
      <Button @click="addImage">
        <svg>
          <use xlink:href="@/assets/sprite.svg#image"/>
        </svg>
      </Button>
      <Button @click="tag" data-tag="h2">
        <svg>
          <use xlink:href="@/assets/sprite.svg#heading-2"/>
        </svg>
      </Button>
      <Button @click="tag" data-tag="h3">
        <svg>
          <use xlink:href="@/assets/sprite.svg#heading-3"/>
        </svg>
      </Button>
      <Button @click="tag" data-tag="h4">
        <svg>
          <use xlink:href="@/assets/sprite.svg#heading-4"/>
        </svg>
      </Button>
      <Button @click="bold">
        <svg>
          <use xlink:href="@/assets/sprite.svg#bold"/>
        </svg>
      </Button>
      <Button @click="align" data-align="justifyCenter">
        <svg>
          <use xlink:href="@/assets/sprite.svg#align-center"/>
        </svg>
      </Button>
      <Button @click="align" data-align="justifyLeft">
        <svg>
          <use xlink:href="@/assets/sprite.svg#align-left"/>
        </svg>
      </Button>
      <Button @click="copyHtml">Скопировать HTML</Button>
    </div>
    <FileInput @change="uploadFile"></FileInput>
    <div contenteditable class="editor" ref="editor">
      Lorem ipsum dolor sit amet, consectetur adipisicing elit. Corporis, recusandae?
    </div>
  </div>
</template>

<script>
import Button from "@/components/Button";
import FileInput from "@/components/FileInput";

export default {
  name: "Wysiwig",
  components: {
    Button,
    FileInput
  },
  methods: {
    tag(event) {
      console.log('tag');
      document.execCommand('formatBlock', false, event.currentTarget.dataset.tag);
    },
    bold() {
      document.execCommand('bold');
    },
    align(event) {
      console.log('align');
      document.execCommand(event.currentTarget.dataset.align);
    },
    copyHtml() {
      const html = this.$refs.editor.innerHTML;
      navigator.clipboard.writeText(html);
      alert(html);
      console.log(html);
    },
    undo() {
      console.log('undo');
      document.execCommand('undo', false, '')
    },
    redo() {
      console.log('redo');
      document.execCommand('redo', false, '')
    },
    addImage() {
      console.log('add image');
      const src = prompt('Введите URL изображения', '');
      if (!src) {
        alert('URL пустой');
      } else {
        console.log('url', src);
        document.execCommand('insertImage', false, src);
      }
    },
    uploadFile(file) {
      const fileUrl = URL.createObjectURL(file);
      this.$refs.editor.focus();
      document.execCommand('insertImage', false, fileUrl);
      console.log('fileUrl', fileUrl);
    }
  }
}
</script>

<style scoped>

.controls {
  display: grid;
  grid-template-columns: repeat(12, auto);
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
