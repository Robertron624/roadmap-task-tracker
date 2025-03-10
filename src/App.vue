<script setup lang="ts">
import { ref } from 'vue'
import TaskForm from './components/TaskForm.vue'
import { createId } from "./utils.ts"
import { Task } from './types.ts'

const tasks = ref<Task[]>([])

const addTask = (title: string) => {
  const newTask: Task = {
    id: createId(12),
    title,
    completed: false,
    createdAt: new Date(),
    priority: 'medium'
  }
  tasks.value.push(newTask)
}
</script>

<template>
  <main>
    <h1 class="title">
      Task tracker
    </h1>
    <TaskForm msg="Hello from App vue" />
  </main>
</template>

<style scoped>
main {
  border: 2px solid #817f7f;
  border-radius: .75rem;
  padding: 2rem 1.5rem;
}
h1.title {
  font-size: 3.5rem;
  font-weight: 800;
  margin-bottom: 2rem;
}
</style>
