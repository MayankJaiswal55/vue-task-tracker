<template>
    <div v-for="task in tasks">
        <Task @toggle-reminder="$emit('toggle-reminder', task.id)"
         @delete-task="$emit('delete-task', task.id)"
            :task="task"></Task>

    </div>
</template>

<script lang="ts">
import type { Task as TaskType } from "./types"
import Task from "./Task.vue";
export default {
    name: "Tasks",
    props: {
        tasks: {
            type: Array as () => TaskType[],
        }
    },
    components: {
        Task,
    },
    emits: ['delete-task','toggle-reminder']
}
</script>