<script setup lang="ts">
import { ref } from 'vue'
import Enter from "./icons/Enter.vue";

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
    <div class="input-wrapper">
      <input v-model="title" type="text" placeholder="Start writing and press enter to create task" />
      <div class="icon">
        <Enter width="1.35rem" height="1.35rem" color="#000" />
      </div>
    </div>
  </form>
</template>

<style scoped>
form {
  display: flex;
  gap: .5rem;
}

.input-wrapper {
  position: relative;
  width: 100%;
}

.input-wrapper .icon {
  position: absolute;
  right: 8px;
  top: 5px;
  background-color: #fff;
  border-radius: .35rem;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 2.5rem;
  height: 2.5rem;
}

input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: .5rem;
  width: 95%;
  height: 2rem;
  font-size: .9rem;
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