<template>
  <label class="label">
    {{ value }}
  </label>
</template>

<script>
export default {
  name: 'Label',
  props: {
    value: String,
  },
};
</script>

<style scoped>
.label {
  display: flex;
  min-width: 100px;
}
</style>
