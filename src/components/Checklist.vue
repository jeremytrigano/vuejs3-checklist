<template>
  <div id="checklist">
    <h1>{{ msg }}</h1>
    <input type="text" v-model="newTodo" /><button
      @click="addTodo"
      v-if="newTodo != ''"
    >
      Ajouter
    </button>
    <br />
    <br />
    <Todo :todos="todos" @delete-todo="deleteTodo" />
  </div>
</template>

<script>
import Todo from './Todo.vue';
import { ref } from 'vue';

export default {
  name: 'Checklist',
  components: {
    Todo,
  },
  setup() {
    let todos = ref([]);
    let newTodo = ref('');

    const addTodo = () => {
      todos.value = [
        ...todos.value,
        {
          todo: newTodo.value,
          id: Date.now(),
        },
      ];
      newTodo.value = '';
    };

    const deleteTodo = (todo) => {
      todos.value = todos.value.filter((t) => t.id !== todo.id);
    };

    return {
      msg: 'Bienvenue sur votre Checklist',
      addTodo,
      deleteTodo,
      todos,
      newTodo,
    };
  },
};
</script>

<style scoped>
#checklist {
  width: 400px;
  margin: auto;
  text-align: center;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  text-align: left;
}
</style>
