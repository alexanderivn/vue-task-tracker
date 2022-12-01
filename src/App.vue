<template>
  <section class="m-auto p-6 ">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask" />
    <div v-if="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <p v-if="(tasks.length > 0)" class="text-xs">double click to set reminder</p>
    <Tasks v-if="(tasks.length > 0)" @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
    <div v-else="(!tasks.length)" class="font-bold text-center py-4 text-gray-500">Ooops, No task found here...</div>
  </section>
</template>


<script>
import AddTask from './components/AddTask.vue';
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';


export default {
  name: 'App',

  components: {
    Header, Tasks, AddTask
  },

  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },

  methods: {
    toggleAddTask() {      
      this.showAddTask = !this.showAddTask;
    },

    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => task.id === id
        ? { ...task, reminder: !task.reminder } : task)
    },

    addTask(task) {
      this.tasks = [...this.tasks, task];
    },

    deleteTask(id) {
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter((task) => task.id !== id)        
      }
    },

    async fetchTasks() {
      const response = await fetch('http://localhost:3000/tasks');
      const data = await response.json();
      return data;

    }
  },

  async created() {
    this.tasks = await this.fetchTasks();
  }
}
</script>

