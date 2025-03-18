<script setup lang="ts">
import { ref, onMounted } from 'vue'
import TaskForm from './components/TaskForm.vue'
import TaskList from './components/TaskList.vue'
import { createId } from "./utils.ts"
import type { Task } from './types.ts'

const defaultTasks: Task[] = [
  { id: createId(12), title: 'Task 1', completed: false, createdAt: new Date(), priority: 'medium' },
  { id: createId(12), title: 'Task 2', completed: false, createdAt: new Date(), priority: 'medium' },
  { id: createId(12), title: 'Task 3', completed: false, createdAt: new Date(), priority: 'medium' },
]

const tasks = ref<Task[]>([])

onMounted(() => {
  tasks.value = [...defaultTasks]
})

const addTask = (title: string) => {
  const newTask: Task = {
    id: createId(12),
    title,
    completed: false,
    createdAt: new Date(),
    priority: 'medium'
  }

  // add the new task to the beginning of the tasks array
  tasks.value = [newTask, ...tasks.value]
}

const deleteTask = (taskId: string) => {
  tasks.value = tasks.value.filter(task => task.id !== taskId)
}

const toggleTask = (taskId: string) => {
  const task = tasks.value.find(task => task.id === taskId)
  if (task) {
    task.completed = !task.completed
    sortTasks()
  }
}

// function to move completed tasks to the bottom of the list
const sortTasks = () => {
  tasks.value.sort((a, b) => {
    if (a.completed && !b.completed) return 1
    if (!a.completed && b.completed) return -1
    return 0
  })
}
</script>

<template>
  <main>
    <h1 class="title">
      Task tracker
    </h1>
    <TaskForm @submit-task="addTask"/>
    <TaskList :tasks="tasks" @delete-task="deleteTask" @toggle-task="toggleTask"/>
  </main>
</template>

<style scoped>
main {
  border: 2px solid #817f7f;
  border-radius: .75rem;
  padding: 2rem 1.5rem;
  width: 35rem;
}
h1.title {
  font-size: 3.5rem;
  font-weight: 800;
  margin-bottom: 2rem;
}
</style>
