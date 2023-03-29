<template>
  <div class="input-wrapper">
    <template v-if="label">
      <Label :value="label" />
    </template>
    <input
      v-bind:value="value"
      v-on:input="$emit('input', $event.target.value)"
      :name="name"
      placeholder="введите данные"
    />
  </div>
</template>

<script>
import Label from '../Label/Label';

export default {
  name: 'Input',
  components: { Label },
  props: {
    label: String,
    name: String,
    value: String,
  },
  comments: { Label },
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
.input-wrapper input {
  width: 150px;
  padding: 5px 8px;
}
</style>
