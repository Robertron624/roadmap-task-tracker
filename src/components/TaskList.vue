<script setup lang="ts">
import { defineProps, defineEmits } from 'vue'
import { Task } from '../types.ts'

defineProps<{ tasks: Task[] }>()
const emit = defineEmits(['delete-task', 'toggle-task'])
</script>

<template>
    <ul class="task-list">
        <li v-for="task in tasks" :key="task.id" class="task-item">
            <div class="left">
                <input type="checkbox" :checked="task.completed" @change="emit('toggle-task', task.id)">
                <span :class="{ completed: task.completed }">{{ task.title }}</span>
            </div>
            <button class="delete-btn" @click="emit('delete-task', task.id)">
                <span class="sr-only">
                    Delete this task
                </span>
                🗑️
            </button>
        </li>
    </ul>
</template>

<style scoped>
.task-list {
    list-style: none;
    padding: 0;
    margin-top: 1rem;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.task-item {
    padding: 0.5rem;
    border-bottom: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
}

.task-item .left {
    display: flex;
    gap: .35rem;
    align-items: center;
}

.task-item .left input {
    width: 1rem;
    height: 1rem;
    cursor: pointer;
}

.task-item .completed {
    text-decoration: line-through;
    color: #777;
}

.delete-btn {
    background: transparent;
    border: none;
    cursor: pointer;
    font-size: 1rem;
    color: rgb(184, 24, 24);
    background-color: #fff;
    padding: .5rem .5rem;
}

.delete-btn:hover {
    color: white;
    background-color: rgb(184, 24, 24);
}
</style>