<template>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <button @click="deleteTodo(todo)">x</button>{{ todo.todo }}
    </li>
  </ul>
</template>

<script>
export default {
  name: 'Todo',
  emits: ['delete-todo'],
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
  setup(props, { emit }) {
    const deleteTodo = (todo) => {
      emit('delete-todo', todo);
    };
    return { deleteTodo };
  },
};
</script>
