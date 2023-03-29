<template>
  <button @click="onClick && onClick()" :class="['button', variant]" :type="type">
    <slot />
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    onClick: Function,
    disabled: Boolean,
    variant: {
      type: String,
      validator(value) {
        return ['primary', 'outlined'].includes(value);
      },
      default: 'primary',
    },
    type: String,
  },
};
</script>

<style scoped>
.button {
  border-radius: 8px;
  padding: 10px 10px;
  width: 150px;
  cursor: pointer;
  color: white;
}

.primary {
  background: rgb(26, 130, 226);
  border: none;
}
.primary:hover {
  background-color: rgb(158, 205, 247);
}

.outlined {
  color: black;
  background: white;
  border: 1px solid rgb(26, 130, 226);
}
.outlined:hover {
  border-color: rgb(158, 205, 247);
}
</style>
