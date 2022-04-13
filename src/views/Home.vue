<template>
  <AddTask @add-task="addTask" v-if="showAddTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTasks"
    :tasks="tasks"
  />
</template>

<script>
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";

export default {
  name: "Home",
  props: {
    showAddTask: {
      type: Boolean,
    },
  },
  components: {
    AddTask,
    Tasks,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    // create
    async addTask(newTask) {
      const res = await fetch("api/tasks", {
        method: "POST",
        body: JSON.stringify(newTask),
        headers: {
          "Content-type": "application/json",
        },
      });
      const data = await res.json();

      this.tasks.push(data);
    },
    // read datas
    async getTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },
    // read a single data
    async getTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
    // update
    async toggleReminder(id) {
      const toggleTask = await this.getTask(id);
      toggleTask.reminder = !toggleTask.reminder;
      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(toggleTask),
      });
      const data = await res.json();
      this.tasks.map((task) => {
        if (task.id === id) task.reminder = data.reminder;
      });
    },
    // delete
    async deleteTasks(id) {
      if (confirm("Are you sure you wanna delete?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });
        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Error in deleteing task.");
      }
    },
  },
  emits: ["delete-task", "toggle-reminder", "add-task"],
  async created() {
    this.tasks = await this.getTasks();
  },
};
</script>
