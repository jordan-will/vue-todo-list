<script setup>

import { ref, defineEmits } from 'vue'
import Button from './Button.vue'

const todo = ref(null)
const emit = defineEmits(['addTodo'])

const addTodo = () => {

  if (!todo.value) {
    alert('Please add a task')
    return
  }

  const newTodo = {
    id: Date.now(),
    task: todo.value,
    completed: false
  }

  emit('addTodo', newTodo)

  todo.value = null

}

</script>

<template>

  <h2 class="app__subtitle">CREATE TODO</h2>

  <input 
    v-model="todo"
    type="text" 
    class="app__input" 
    placeholder="Add your task" />

  <Button label="Add Todo" @btnClicked="addTodo" />

</template>