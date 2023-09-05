<script lang="ts" setup>
import { nanoid } from 'nanoid';
import type { Column } from '~~/types'
import draggable from 'vuedraggable'


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
  <div>
    <draggable
      v-model="columns"
      group="columns"
      item-key="id"
      class="flex gap-4 overflow-x-auto items-start"
      :animation="150"
      handle=".drag-handle"
    >
      <template #item="{ element: column }: { element: Column }">
        <div class="column bg-gray-200 p-5 rounded min-w-[250px]">
          <header class="font-bold mb-4 flex gap-2 items-center">
            <span class="drag-handle cursor-pointer">
              ⠏
            </span>
            {{ column.title }}
          </header>
          <TrelloBoardTask
            v-for="   task    in    column.tasks   "
            :key=" task.id "
            :task=" task "
          />
          <footer>
            <button class="text-gray-500">+ Add a Card</button>
          </footer>
        </div>
      </template>

    </draggable>
  </div>
</template>

<style scoped></style>
