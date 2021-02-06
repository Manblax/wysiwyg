<template>
  <div class="upload" style="margin-top: 20px;">
    <input type="file" @change="onChange" name="file" ref="input" id="file"/>
    <label for="file" class="button button--primary upload__button" ref="label">
      Выберите файл
    </label>
    <span class="upload__caption">Файл не выбран</span>
  </div>
</template>

<script>
export default {
  name: "FileInput",
  data() {
    return {
      default: 'Выберите файл'
    }
  },
  methods: {
    onChange(event) {
      let fileName = '';
      if (this.$refs.input.files && this.$refs.input.files.length > 1) {
        fileName = (
          this.$refs.input.getAttribute('data-multiple-caption') || ''
        )
          .replace('{count}', this.$refs.input.files.length);
      } else {
        fileName = event.target.value.split('\\')
          .pop();
      }

      if (fileName) {
        this.$refs.label.nextElementSibling.innerHTML = fileName;
      } else {
        this.$refs.label.innerHTML = this.default;
      }
      this.$emit('change', event.target.files[0]);
    }
  }
}
</script>

<style scoped>
.button {
  font-family: inherit;
  font-size: 1rem;
  line-height: 1.5;

  display: inline-block;
  padding: 9px 20px;
  cursor: pointer;
  transition-timing-function: ease;
  transition-duration: .25s;
  transition-property: background-color, border-color, box-shadow;
  text-decoration: none;
  border-radius: 4px;
  margin: 0;
  box-shadow: none;
}

.button--primary {
  color: white;
  border: 1px solid var(--action-element-color);
  background-color: var(--action-element-color);
}

.button--primary:hover {
  border-color: #0055bf;
  outline: none;
  background-color: #0055bf;
}

.button--primary:focus {
  border-color: var(--action-element-color);
  outline: none;
  background-color: var(--action-element-color);
  box-shadow: 0 0 0 3px rgba(0, 97, 217, .5);
}

.button--primary:active {
  border-color: #004aa6;
  background-color: #004aa6;
  box-shadow: none;
}

[type='file'] {
  position: absolute;
  z-index: -1;
  overflow: hidden;
  width: 0;
  height: 0;
  opacity: 0;
}

[type='file']:focus + label,
[type='file'].focus + label {
  box-shadow: 0 0 0 3px rgba(0, 97, 217, .5);
}

[type='file'] + label * {
  pointer-events: none;
}

.upload {
  font-weight: 400;
  display: inline-flex;
  align-items: center;
  margin-top: 8px;
  padding: 28px;
  color: blue;
  border: 1px solid blue;
  background-color: transparent;
}

.upload__button {
  flex-shrink: 0;
  margin-right: 28px;
  background-color: transparent;
}

.upload__caption {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

</style>
