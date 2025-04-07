<script setup>

import { defineProps, defineEmits, computed } from 'vue'
import Button from './Button.vue'

const props = defineProps({
  todoList: Array
})

const emit = defineEmits(['deleteTodo'])

const deleteTodo = (id) => {
  emit('deleteTodo', id)
}

const updateTodo = (id) => {
  const index = todoList.value.findIndex(todo => todo.id === id)
  if (index !== -1) {
    todoList.value[index].completed = !todoList.value[index].completed
  }
}

const sortedTodoList = computed(() => {
  return props.todoList.slice().sort((a, b) => Number(a.completed) - Number(b.completed));
});


</script>

<template>

  <h2 class=" app__subtitle app__subtitle--list">TODO LIST</h2>

  <ul class="app__list">
    <li class="app__list-item" v-for="todo in sortedTodoList" :key="todo.id">
      <label class="app__list-label">
        <input type="checkbox" class="app__checkbox" v-model="todo.completed" :checked="todo.completed"
          @change="updateTodo(todo.id)" />
        <span class="app__label">{{ todo.task }}</span>
      </label>
      <Button label="Delete" @btnClicked="deleteTodo(todo.id)" />
    </li>

  </ul>

</template>