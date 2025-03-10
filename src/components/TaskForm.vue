<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()

const count = ref(0)
</script>

<template>
  <p>
    This is the message: 
  </p>
  <h1 class="message">{{ msg }}</h1>

</template>

<style scoped>
.message {
  color: #888;
}
</style>
