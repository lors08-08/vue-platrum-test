<template>
  <div class="wrapper">
    <div :class="[isChild && 'child', 'col1']" @click="onClick && onClick()">{{ col1 }}</div>
    <div class="col2" @click="onClick && onClick()">{{ col2 }}</div>
  </div>
</template>

<script>
export default {
  name: 'Element',
  props: {
    onClick: Function,
    col1: String,
    col2: String,
    isChild: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style scoped>
  .wrapper {
    display: flex;
    justify-content: flex-end;
    height: fit-content;
    color: black;
  }
  .col1 {
    width: 40%;
    border: 1px solid #e8e8e8;
    cursor: pointer;
  }
  .col2 {
    width: 60%;
    border: 1px solid #e8e8e8;
    cursor: pointer;
  }
  .child {
    width: 30%;
  }
</style>
