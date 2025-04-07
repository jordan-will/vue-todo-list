<script setup>

  import {ref, defineProps} from 'vue'

  defineProps({
    completedTask: [Number, String],
    pendingTask: [Number, String]
  })

</script>

<template>
  <h2 class="app__subtitle app__subtitle--status">STATUS</h2>

  <div class="app__status">
    <div class="app__status-item app__status-item--completed">
      <span class="app__status-count">{{ completedTask }}</span>
      <span class="app__status-label">Completed</span>
    </div>
    <div class="app__status-item app__status-item--pending">
      <span class="app__status-count">{{ pendingTask }}</span>
      <span class="app__status-label">Pending</span>
    </div>
  </div>
</template>