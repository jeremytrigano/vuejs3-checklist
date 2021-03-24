<template>
  <div id="checklist">
    <h1>{{ msg }}</h1>
    Ajouter un nouveauToDo :
    <input
      class="mb-1"
      type="text"
      v-model="newTodo"
      @keypress.enter="addTodo"
    />&nbsp;
    <div class="buttonDiv">
      <button
        class="action-button shadow animate blue"
        @click="addTodo"
        v-if="newTodo != ''"
      >
        Ajouter
      </button>
    </div>
    <br />
    <Todo :todos="todos" @delete-todo="deleteTodo" @edit-todo="editTodo" />
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

    const editTodo = (todo) => {
      todos.value = todos.value.map((t) => (t.id !== todo.id ? t : todo));
    };

    const deleteTodo = (todo) => {
      todos.value = todos.value.filter((t) => t.id !== todo.id);
    };

    return {
      msg: 'Bienvenue sur votre Checklist',
      addTodo,
      editTodo,
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

.buttonDiv {
  height: 40px;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  text-align: left;
}

.mb-1 {
  margin-bottom: 1em;
}

::v-deep .animate {
  transition: all 0.1s;
  -webkit-transition: all 0.1s;
}

::v-deep .action-button {
  position: relative;
  padding: 1px 7px;
  margin: 0px 10px 10px 0px;
  border-radius: 5px;
  font-family: 'Pacifico', cursive;
  color: #fff;
  text-decoration: none;
  border-style: none;
  outline-style: none;
}

::v-deep .blue {
  background-color: #3498db;
  border-bottom: 5px solid #2980b9;
  text-shadow: 0px -2px #2980b9;
}

::v-deep .red {
  background-color: #e74c3c;
  border-bottom: 5px solid #bd3e31;
  text-shadow: 0px -2px #bd3e31;
}

::v-deep .green {
  background-color: #82bf56;
  border-bottom: 5px solid #669644;
  text-shadow: 0px -2px #669644;
}

::v-deep .action-button:active {
  transform: translate(0px, 5px);
  -webkit-transform: translate(0px, 5px);
  border-bottom: 1px solid;
}
</style>
