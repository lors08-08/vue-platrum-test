<template>
  <div class="input-wrapper">
    <template v-if="label">
      <Label :value="label" />
    </template>
    <select
      v-bind:value="value"
      v-on:input="$emit('input', $event.target.value)"
    >
      <slot />
    </select>
  </div>
</template>

<script>
import Label from '../Label/Label';

export default {
  name: 'Selector',
  components: { Label },
  props: {
    label: String,
    name: String,
    value: String,

  },
};
</script>

<style scoped>
.input-wrapper {
  display: flex;
  column-gap: 10px;
}
.input-wrapper input {
  border: none;
  padding: 0;
}
.input-wrapper select {
  width: 150px;
  padding: 5px 8px;
  box-sizing: content-box;
}
</style>
