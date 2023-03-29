<template>
  <div class="wrapper">
    <Element :onClick="toggleSort" col1="Имя" col2="Телефон" />
    <template v-for="dataSet in data">
      <Element
        v-if="!('parentId' in dataSet)"
        :key="dataSet.id"
        :col1="dataSet.name"
        :col2="dataSet.phone"
      />
      <template v-for="child in data.filter((e) => e.parentId === dataSet.id)">
        <Element
          :key="child.id"
          :col1="child.name"
          :col2="child.phone"
          is-child
        />
      </template>
    </template>
  </div>
</template>

<script>
import Element from './components/Element';

export default {
  name: 'Table',
  components: { Element },
  methods: {
    toggleSort() {
      this.$emit('toggle-sort');
    },
  },
  props: {
    data: Array,
  },
};
</script>

<style scoped>
.wrapper {
  height: 300px;
  width: 500px;
}
</style>
