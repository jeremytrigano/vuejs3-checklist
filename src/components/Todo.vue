<template>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <button
        class="action-button shadow animate red"
        @click="deleteTodo(todo)"
      >
        x
      </button>
      <button class="action-button shadow animate blue" @click="editTodo(todo)">
        Editer
      </button>
      &nbsp;<span v-if="todoToEdit !== null && todoToEdit.id === todo.id">
        <input
          type="text"
          v-model="todoToEdit.todo"
          @keypress.enter="save"
        />&nbsp;<button
          class="action-button shadow animate green"
          @click="save"
        >
          Sauvegarder
        </button> </span
      ><span v-else>{{ todo.todo }}</span>
    </li>
  </ul>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'Todo',
  emits: ['delete-todo', 'edit-todo'],
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
  setup(props, { emit }) {
    let todoToEdit = ref(null);

    const deleteTodo = (todo) => {
      emit('delete-todo', todo);
    };
    const editTodo = (todo) => {
      todoToEdit.value = todo;
    };
    const save = () => {
      emit('edit-todo', todoToEdit.value);
      todoToEdit.value = null;
    };
    return { deleteTodo, editTodo, save, todoToEdit };
  },
};
</script>

<style scoped></style>
