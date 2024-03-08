<template>
    <div @dblclick="$emit('toggle-reminder', task?.id)" :class="[task?.reminder ? 'reminder' : '', 'task']">
        <h3>{{ task?.text }}
            <i v-if="task && task.id !== undefined" @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
        </h3>
        <p>{{ task?.id }}</p>
    </div>
</template>

<script lang="ts">
// import Tasks from './Tasks.vue';
import type { Task } from './types';
export default {
    name: "Task",
    props: {
        task: Object as () => Task,
    },
    emits: ['delete-task', 'toggle-reminder']
}

</script>

<style scoped>
.fas {
    color: red;
}

.task {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
}

.task.reminder {
    border-left: 5px solid green;
}

.task h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>