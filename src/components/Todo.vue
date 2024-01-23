<script setup>
import { onMounted, ref } from 'vue'

defineProps({
  msg: String
})

const TodoList = ref([])

function addTodo(task) {
  TodoList.value.push(task)
  localStorage.setItem('TodoList', JSON.stringify(TodoList.value))
}

function deleteTodo(todo) {
  const index = TodoList.value.indexOf(todo)
  TodoList.value.splice(index, 1)
  localStorage.setItem('TodoList', JSON.stringify(TodoList.value))
}

onMounted(() => {
  const storage = JSON.parse(localStorage.getItem('TodoList'))
  TodoList.value = storage
  console.log(storage)
  console.log(typeof localStorage)
})
</script>

<template>
  <h1>{{ msg }}</h1>
  <div class="addTodoBlock">
    <input 
  type="text" 
  class="inputTodo" 
  v-model="task" 
  placeholder="Впишите задачу" 
  @keyup.enter="addTodo(task); task = '';"
  >
  <button @click="addTodo(task); task = '';">Добавить</button>
  </div>
  
  <ul v-if="TodoList.length > 0">
    <li v-for="todo in TodoList">
      <button @click="deleteTodo(todo)">
        {{ todo }}
      </button>
    </li>
  </ul>
  <p v-else>Нету задач</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}

.inputTodo {
  border-radius: 5px;
  padding: .2rem;
  font-weight: bold;
  font-size: .8rem;
  margin-right: 12px;
  margin-left: 12px;
  border: none;
  outline: none;
}

.inputTodo::placeholder {
  font-weight: bold;
}

.addTodoBlock {
  display: flex;
  justify-content: center;
  height: 2rem;
  text-align: center;
}

li {
  list-style: none;
}
</style>
