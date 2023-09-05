<script lang="ts" setup>
import { nanoid } from 'nanoid';
import type { Column } from '~~/types'

const columns = ref<Column[]>([
  {
    id: nanoid(),
    title: 'Backlog',
    tasks: [
      { id: nanoid(), title: "Create marketing landing page", createdAt: new Date() },
      { id: nanoid(), title: "Add SEO keywords", createdAt: new Date() },
      { id: nanoid(), title: "Add Google Analytics", createdAt: new Date() }
    ]
  },
  { title: "selected for Dev", id: nanoid(), tasks: [] },
  { title: "In Progress", id: nanoid(), tasks: [] },
  { title: "QA", id: nanoid(), tasks: [] },
  { title: "Complete", id: nanoid(), tasks: [] }
])

</script>

<template>
  <div class=" flex gap-4 overflow-x-auto items-start">
    <div
      class="column bg-gray-200 p-5 rounded min-w-[250px]"
      v-for="column in columns"
      :key="column.id"
    >
      <header>{{ column.title }}</header>
      <p
        v-for="task in column.tasks"
        :key="task.id"
      >
        {{ task.title }}</p>
    </div>
  </div>
</template>

<style scoped></style>
