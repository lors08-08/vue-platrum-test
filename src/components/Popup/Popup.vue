<template>
  <div class="wrapper">
    <div class="header">
      <div>Добавить пользователя</div>
      <div class="close-wrapper" @click="togglePopup">
        <i class="fas fa-times"></i>
      </div>
    </div>
    <form class="actions" @submit="onSubmit">
      <Input v-model="name" name="name" label="Имя" />
      <Input v-model="phone" name="phone" label="Номер" />
      <Selector v-model="selectedValue" name="selectedValue" label="Начальник">
        <option disabled value="" selected>Выберите один из вариантов</option>
        <template v-for="element in data.filter(e => !('parentId' in e))">
          <option :key="element.id" :value="element.id">{{
            element.name
          }}</option>
        </template>
      </Selector>
      <div class="btn-wrapper">
        <Button type="submit" variant="outlined">Добавить</Button>
      </div>
    </form>
  </div>
</template>

<script>
import { v4 as uuid4 } from 'uuid';
import Button from '../ui/Button/Button';
import Input from '../ui/Input/Input';
import Selector from '../ui/Selector/Selector';

export default {
  name: 'Popup',
  components: { Selector, Input, Button },
  emits: ['togglePopup'],
  data() {
    return {
      name: '',
      phone: '',
      selectedValue: '',
    };
  },
  props: {
    data: Array,
  },
  methods: {
    togglePopup() {
      this.$emit('toggle-popup');
    },
    onSubmit(e) {
      e.preventDefault();

      if (!this.name || !this.phone) {
        // eslint-disable-next-line no-alert
        alert('Имя или Телефон не могут быть пустыми');
        return;
      }

      const newElement = {
        id: uuid4(),
        name: this.name,
        phone: this.phone,
      };

      if (this.selectedValue) {
        newElement.parentId = this.selectedValue;
      }

      this.$emit('add-element', newElement);

      this.togglePopup();
    },
  },
};
</script>

<style scoped>
.wrapper {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);

  box-shadow: 0 11px 10px #aaaaaa;
  height: fit-content;
  background-color: #e8e8e8;
  border-radius: 8px;
  min-width: 400px;
}
.header {
  display: flex;
  justify-content: space-between;
  padding: 10px 24px;
}

.actions {
  padding: 24px;

  display: flex;
  flex-direction: column;
  row-gap: 10px;
  align-items: center;
}
.btn-wrapper {
  display: flex;
  justify-content: flex-end;
  padding-top: 20px;
}
.close-wrapper {
  cursor: pointer;
}
.close-wrapper i {
  color: #ed6a5e;
}
</style>
