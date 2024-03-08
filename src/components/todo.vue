<script setup>
import { ref } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faXmark } from '@fortawesome/free-solid-svg-icons' // Import specific icon

// give each todo a unique id

let id = 0

const newTodo = ref('')
const todos   = ref([
    {
        id: id++, text: 'Learn Vue'
    }
])
function addTodo() {
    todos.value.push({id:id++, text:newTodo.value})
    newTodo.value = ''
}
function removeTodo(todo) {
    todos.value = todos.value.filter((t) => t !== todo)

}
</script>

<template>
  <div class="todo-list">
    <form @submit.prevent="addTodo" class="todo-form">
      <input v-model="newTodo" required placeholder="New todo" class="todo-input">
      <button type="submit" class="todo-add-btn">Add Todo</button>
    </form>
    <ul class="todo-items">
      <li v-for="todo in todos" :key="todo.id" class="todo-item">
        {{ todo.text }}
        <button @click="removeTodo(todo)" class="todo-remove-btn">
          <font-awesome-icon :icon="faXmark" />
        </button>
      </li>
    </ul>
  </div>
</template>


<style scoped>
.todo-list {
    font-family: Arial, sans-serif;
    max-width: 400px;
    margin: 0 auto;
}

form {
    margin-bottom: 10px;
}

input[type="text"] {
    padding: 5px;
    width: 200px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    padding: 5px 10px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    margin-bottom: 5px;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 4px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

button.remove-todo {
    background-color: transparent;
    border: none;
    cursor: pointer;
    font-size: 14px;
    color: #d9534f; /* Red color for delete button */
}

button.remove-todo:hover {
    color: #c9302c;
}
</style>