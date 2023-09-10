<script lang="ts" setup>
import {nanoid} from 'nanoid';
import type {Column, Task} from '~~/types'
import draggable from 'vuedraggable'


const columns = ref<Column[]>([
    {
        id: nanoid(),
        title: 'Backlog',
        tasks: [
            {id: nanoid(), title: "Create marketing landing page", createdAt: new Date()},
            {id: nanoid(), title: "Add SEO keywords", createdAt: new Date()},
            {id: nanoid(), title: "Add Google Analytics", createdAt: new Date()}
        ]
    },
    {title: "selected for Dev", id: nanoid(), tasks: []},
    {title: "In Progress", id: nanoid(), tasks: []},
    {title: "QA", id: nanoid(), tasks: []},
    {title: "Complete", id: nanoid(), tasks: []}
])

const altPressed = useKeyModifier('Alt')


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
                <div class="column bg-gray-200 p-5 rounded w-[250px]">
                    <header class="font-bold mb-4 flex gap-2 items-center">
                        <TrelloBoardDragHandle/>
                        {{ column.title }}
                    </header>
                    <draggable
                            v-model=" column.tasks "
                            :group="
              { name: 'tasks', pull: altPressed ? 'clone' : true }
            "
                            item-key="id"
                            :animation=" 150 "
                            handle=".drag-handle"
                    >
                        <template #item=" { element: task }: { element: Task } ">
                            <div class="flex gap-2 items-start">
                                <TrelloBoardDragHandle/>
                                <TrelloBoardTask :task=" task "/>
                            </div>
                        </template>

                    </draggable>
                    <footer>
                        <NewTask @add="column.tasks.push($event)"/>
                    </footer>
                </div>
            </template>

        </draggable>
    </div>
</template>

<style scoped>
.sortable-drag .task {
    transform: rotate(2deg);
}

.sortable-ghost .task {
    position: relative
}

.sortable-ghost .task::after {
    content: '';
    @apply absolute inset-0 bg-slate-300 rounded
}
</style>
