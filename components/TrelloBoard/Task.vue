<script setup lang="ts">
import type { Task } from '~~/types'

defineProps<{
  task: Task
}>()

</script>

<template>
  <div
    class="task bg-white p-2 mb-2 rounded shadow-sm w-full"
    :title="task.createdAt.toLocaleDateString()"
  >
    {{ task.title }}
  </div>
</template>



<style scoped></style>