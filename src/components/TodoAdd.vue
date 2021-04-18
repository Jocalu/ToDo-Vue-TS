<template>
  <div id="add-container">
    <form @submit="addTodo">
      <input
        type="text"
        v-model="title">
    </form>
  </div>
</template>

<script lang="ts">
import { uuid } from 'vue-uuid';

interface Data {
  title: string
}

export default {
  name: 'TodoAdd',
  data(): Data {
    return {
      title: '',
    };
  },
  methods: {
    addTodo(event: Event): void {
      event.preventDefault();

      const newTodo = {
        id: uuid.v4(),
        title: this.title,
        completed: false,
      };
      this.title = '';
      this.$emit('add-todo', newTodo);
    },
  },
};
</script>

<style lang="scss">
  #add-container{
    padding: 10px;
  }
  input {
    padding: 10px;
    outline: none;
    border: 1px solid #ccc;
    width: 100%;
  }
</style>
