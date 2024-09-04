<template>
  <div>
    <h1>To Do</h1>
    <p> Things to Do Every Day</p>

    <input v-model="filterText" placeholder="Filter tasks" />
    <select v-model="sortKey">
      <option value="title">Sort by Task</option>
      <option value="completed">Sort by Completion Status</option>
      <option value="incomplete">Sort by Incomplete Status</option> <!-- Updated option text -->
    </select>
    <ul>
      <li v-for="task in sortedTasks" :key="task.id">
        {{ task.title }} - {{ task.completed ? "Completed" : "Incomplete" }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      tasks: [],
      filterText: '',
      sortKey: 'title',
    };
  },
  created() {
    this.fetchTasks();
  },
  methods: {
    async fetchTasks() {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/todos');
        this.tasks = response.data;
      } catch (error) {
        console.error("There was an error fetching the tasks!", error);
      }
    },
  },
  computed: {
    filteredTasks() {
      return this.tasks.filter(task =>
        task.title.toLowerCase().includes(this.filterText.toLowerCase())
      );
    },
    sortedTasks() {
      return this.filteredTasks.slice().sort((a, b) => {
        if (this.sortKey === 'title') {
          return a.title.localeCompare(b.title);
        } else if (this.sortKey === 'completed') {
          return a.completed === b.completed ? 0 : a.completed ? -1 : 1;
        } else if (this.sortKey === 'incomplete') {
          return a.completed === b.completed ? 0 : a.completed ? 1 : -1; // Reverse sort order for incomplete
        } else {
          return 0;
        }
      });
    }
  }
};
</script>
