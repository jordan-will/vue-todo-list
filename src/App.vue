<script setup>

import { ref, onMounted, computed, watch } from 'vue'
import AddTodo from './components/AddTodo.vue'
import StatusTask from './components/StatusTask.vue'
import TaskList from './components/TaskList.vue'

const todoList = ref([])

const completedTask = computed(()=>{
    return todoList.value.filter(todo =>todo.completed).length  
})

const pedingTask = computed(()=>{
    return todoList.value.filter(todo=>!todo.completed).length
})

const addTodo = (todo) =>{
  todoList.value.unshift(todo)
}

const deleteTodo = (id) => {
  todoList.value = todoList.value.filter(todo => todo.id !== id)
}

onMounted(()=>{
  const storedTodos = localStorage.getItem('todoList')
  todoList.value = JSON.parse(storedTodos) || []
})

watch(todoList, (newTodoList) => {
  localStorage.setItem('todoList', JSON.stringify(newTodoList))
}, { deep: true })

</script>

<template>

  <div class="app">
    <h1 class="app__title">Vue Tasks</h1>
    
    <AddTodo @addTodo="addTodo" />
    
    <StatusTask :completedTask="completedTask" :pendingTask="pedingTask" />

    <TaskList v-if="todoList.length > 0" :todoList="todoList" @deleteTodo="deleteTodo" />

  </div>

</template>

<style scoped></style>
