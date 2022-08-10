<template>
  <div class="hello">
    <form @submit.prevent="addNewTodo">
      <label>New todo</label>
      <input v-model="newTodo" name="newTodo" />
      <button>Add new Todo</button>
    </form>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id">
        <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
          {{ todo.content }}
        </h3>
        <button @click="removeTodo(index)">Remove Todo</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "todo",
  setup() {
    const todos = ref([]);
    const newTodo = ref("");

    const addNewTodo = () => {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    };
    const toggleDone = (todo) => {
      todo.done = !todo.done;
    };
    const removeTodo = (index) => {
      todos.value.splice(index, 1);
    };
    return {
      toggleDone,
      todos,
      newTodo,
      addNewTodo,
      removeTodo,
    };
  },
};
</script>


<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
.done {
  text-decoration: line-through;
}
</style>
