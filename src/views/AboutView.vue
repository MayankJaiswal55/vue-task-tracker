<template>
  <div class="about">
    <div class="container">
      <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"></Header>
      <div v-show="showAddTask">
        <AddTask @add-task="addTask"></AddTask>
      </div>
      <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"></Tasks>
    </div>
  </div>
</template>

<script lang="ts">
import Header from '@/components/Header.vue';
import Tasks from '@/components/Tasks.vue';
import AddTask from '@/components/AddTask.vue';
import type { Task } from '@/components/types';

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [] as Task[],
      showAddTask: false
    }
  },
  methods: {
    addTask(task: Task) {
      this.tasks = [...this.tasks, task]
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    deleteTask(id: Task['id']) {
      if (confirm("Are you sure")) {
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    toggleReminder(id: Task['id']) {
      this.tasks = this.tasks.map((task) => task.id === id ?
        { ...task, reminder: !task.reminder } : task)
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Task 1',
        reminder: true,
      },
      {
        id: 2,
        text: 'Task 2',
        reminder: false,
      },
    ]
  }
}

</script>

<style>

</style>
