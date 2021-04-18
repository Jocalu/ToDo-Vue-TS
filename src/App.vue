<template>
  <div>
    <div id ="header">
      <Search v-on:query-change="querySearch"/>
    </div>
    <div id ="main-container">
      <h2>Todos</h2>
      <TodoAdd v-on:add-todo="addTodo"/>
      <Todos
        v-bind:todoslist="copyTodos"
        v-on:delete-todo="deleteTodo" />
    </div>
  </div>
</template>

<script lang="ts">
import Search from './components/Search.vue';
import Todos from './components/Todos.vue';
import TodoAdd from './components/TodoAdd.vue';

interface todos {
  id: number,
  title: string,
  completed: boolean
}

interface data {
  todos: todos[],
  copyTodos: todos[],
}

export default {
  name: 'App',
  components: {
    Todos, TodoAdd, Search,
  },
  methods: {
    deleteTodo(id: number): void {
      this.todos = this.todos.filter((todo) => todo.id !== id);
      this.copyTodos = [...this.todos];
    },
    addTodo(todo: todos): void {
      this.todos.push(todo);
      this.copyTodos = [...this.todos];
    },
    querySearch(query: string): void {
      if (query === '') {
        this.copyTodos = [...this.todos];
      } else {
        const temporal = this.todos.filter((todo) => todo.title.includes(query));
        this.copyTodos = [...temporal];
      }
    },
  },
  data(): data {
    return {
      todos: [
        {
          id: 0,
          title: 'comprar la cena',
          completed: false,
        },
        {
          id: 1,
          title: 'sacar al perro',
          completed: true,
        },
        {
          id: 2,
          title: 'comprar',
          completed: false,
        },
      ],
      copyTodos: [],
    };
  },
  created(): void {
    this.copyTodos = [...this.todos];
  },
};

</script>

<style lang="scss">
  *,
  *:before,
  *:after {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    font-size: 1.5em;
    padding: 0;
    margin: 0;
    #header {
      background: black;
      padding: 10px;
      h2 {
        padding: 0 10px;
      }
    }
    #main-container {
      border: solid 1px #ccc;
      width: 600px;
      margin: 100px auto;
    }
  }
</style>
