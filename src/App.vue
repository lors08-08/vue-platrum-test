<template>
  <div id="app">
    <Popup
      v-if="isPopupOpen"
      @toggle-popup="togglePopup"
      @add-element="addElement"
      :data="data"
    />
    <div class="wrapper-table">
      <Table :data="data" @toggle-sort="toggleSort" />
      <Button :onClick="togglePopup">Добавить</Button>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import Table from './components/Table/Table';
import Popup from './components/Popup/Popup';
import Button from './components/ui/Button/Button';

export default {
  name: 'App',
  components: {
    Button,
    Table,
    Popup,
  },
  methods: {
    toggleSort() {
      if (this.isSorted) {
        this.data.sort((x, y) => {
          if (y.name < x.name) { return -1; }
          if (x.name > y.name) { return 1; }
          return 0;
        });

        this.isSorted = false;
      } else {
        this.data.sort((x, y) => {
          if (x.name < y.name) { return -1; }
          if (y.name > x.name) { return 1; }
          return 0;
        });

        this.isSorted = true;
      }
    },
    addElement(element) {
      this.data = [...this.data, element];

      window.localStorage.setItem('table-data', JSON.stringify(this.data));
    },
    togglePopup() {
      this.isPopupOpen = !this.isPopupOpen;
    },
  },
  data() {
    return {
      data: [],
    };
  },
  created() {
    const tableData = window.localStorage.getItem('table-data');

    if (!tableData) {
      window.localStorage.setItem('table-data', JSON.stringify([]));
    }

    this.data = JSON.parse(tableData) || [];
  },
  setup() {
    const isPopupOpen = ref(false);
    const isSorted = ref(false);

    return {
      Popup,
      isPopupOpen,
      isSorted,
    };
  },
};
</script>

<style scoped>
.wrapper-table {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding-bottom: 20px;
}
#app {
  position: relative;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
}
</style>
