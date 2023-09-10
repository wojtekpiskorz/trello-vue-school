<script setup lang="ts">
import type {Task} from '~~/types'

defineProps<{
    task: Task
}>()

</script>

<template>
  <div
    class="mb-2 rounded bg-white p-2 shadow-sm   task w-[250px]"
    :title="task.createdAt.toLocaleDateString()"
  >
    {{ task.title }}
  </div>
</template>


<style scoped></style>