<script setup>
  import { defineEmits, defineProps } from 'vue';

  defineProps({
    label: String
  })

  const emit = defineEmits(['btnClicked'])

</script>

<template>
   <button 
   @click="emit('btnClicked')"
   class="app__button app__button--add">{{ label }}</button>
</template>