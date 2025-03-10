<script setup lang="ts">
import { ref } from 'vue'

const emit = defineEmits<(event: 'submit-task', title: string) => void>()

const title = ref('')

const handleSubmit = () => {
  if (!title.value.trim()) return
  emit('submit-task', title.value)
  title.value = ''
}
</script>

<template>
  <form @submit.prevent="handleSubmit">
    <input v-model="title" type="text" placeholder="New Task" />
    <button type="submit">Add Task</button>
  </form>
</template>

<style scoped>
form {
  display: flex;
  gap: .5rem;
}
input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: .5rem;
  width: 70%;
}
button {
  padding: 8px;
  border: 2px solid #007bff;
  background-color: transparent;
  color: #007bff;
  border-radius: .5rem;
  cursor: pointer;
  width: 30%;
}

button:hover {
  background-color: #007bff;
  color: #fff;
}
</style>