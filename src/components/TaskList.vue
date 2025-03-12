<script setup lang="ts">
import { defineProps, defineEmits } from 'vue'
import type { Task } from '../types.ts'
import TrashBin from "./icons/TrashBin.vue";

defineProps<{ tasks: Task[] }>()
const emit = defineEmits(['delete-task', 'toggle-task'])
</script>

<template>
    <ul class="task-list">
        <li v-for="task in tasks" :key="task.id" class="task-item">
            <div class="left">
                <input type="checkbox" class="checkbox" :checked="task.completed" @change="emit('toggle-task', task.id)"
                    :data-tooltip="task.completed ? 'Mark as pending' : 'Mark as completed'">
                <span :class="{ completed: task.completed }">{{ task.title }}</span>
            </div>
            <button class="delete-btn" @click="emit('delete-task', task.id)" data-tooltip="Delete task">
                <span class="sr-only">
                    Delete this task
                </span>
                <TrashBin width="1.35rem" height="1.35rem" color="#000"/>
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

.task-item .left .checkbox {
    width: 1rem;
    height: 1rem;
}

/* Tooltip general */
[data-tooltip] {
    position: relative;
    cursor: pointer;
}

[data-tooltip]::after {
    content: attr(data-tooltip);
    visibility: hidden;
    opacity: 0;
    position: absolute;
    background-color: rgba(0, 0, 0, 0.75);
    color: white;
    padding: 4px 8px;
    border-radius: 4px;
    font-size: 0.75rem;
    bottom: 150%;
    left: 50%;
    transform: translateX(-50%);
    white-space: nowrap;
    transition: opacity 0.2s ease-in-out, visibility 0.2s;
    pointer-events: none;
}

/* Show tooltip on hover */
[data-tooltip]:hover::after {
    visibility: visible;
    opacity: 1;
}


.task-item .completed {
    text-decoration: line-through;
    color: #777;
}

.delete-btn {
    border: none;
    cursor: pointer;
    font-size: 1rem;
    background-color: #fff;
    padding: .5rem .5rem;
    position: relative;
  transition: all .5s ease-in;
}

.delete-btn img {
  width: 1rem;
  height: 1rem;
}

.delete-btn:hover {
    background-color: #ee5f5f;
}
</style>