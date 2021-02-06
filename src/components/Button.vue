<template>
  <button class="image-button image-button--primary" @click="onClick">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "Button",
  methods: {
    onClick(event){
      this.$emit('click', event);
    }
  }
}
</script>

<style scoped>
.image-button {
  font-family: inherit;
  display: inline-flex;
  align-items: center;
  vertical-align: middle;

  padding: 0;
  cursor: pointer;

  border: none;

  background-color: transparent;
  box-shadow: none;
  font-size: 1rem;
  line-height: 1.5;
  text-decoration: none;
  transition: opacity 150ms ease-in-out;
}

.image-button:focus {
  outline: none;
}

.image-button svg {
  display: block;

  width: 24px;
  height: 24px;
  flex-shrink: 0;
}

.image-button svg + span {
  margin-left: 8px;
}

.image-button--primary {
  color: var(--action-element-color);
}

.image-button--primary:hover {
  opacity: .7;
}

.image-button--primary svg {
  fill: var(--action-element-color);
}

.image-button--primary:hover {

}

</style>
