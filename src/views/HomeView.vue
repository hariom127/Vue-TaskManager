<template>
  <AddTaskComponent v-show="showAddTask" @add-task="addTask" />
  <TasksComponent @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks" />
</template>

<script>
// @ is an alias to /src
import TasksComponent from '@/components/TasksComponent.vue'
import AddTaskComponent from '@/components/AddTaskComponent.vue'

export default {
  name: 'HomeView',
  props: {
    showAddTask: Boolean,
  },
  components: {
    TasksComponent,
    AddTaskComponent
  },
  data() {
    return {
      tasks: []
    }
  },
  async created() {
    this.tasks = await this.fetchTasks()
  },
  methods: {
    async addTask(task) {
      console.log("ffff", task);
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(task)
      });
      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },

    async deleteTask(id) {
      if (confirm('Are you sure ?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE'
        });

        res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert('Error in deleting task');
      }
    },

    async toggleReminder(id) {
      const taskData = await this.fetchTask(id);

      const updatedTask = {
        ...taskData,
        reminder: !taskData.reminder
      };

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(updatedTask)
      })
      if (res.status === 200) {
        this.tasks = this.tasks.map((task) => {
          if (task.id === id) {
            task.reminder = !task.reminder;
          }
          return task;
        })
      } else {
        alert('Error in update')
      }
    },

    async fetchTasks() {
      const res = await fetch('api/tasks');
      const data = await res.json();
      return data;
    },

    async fetchTask(id) {
      const task = await fetch(`api/tasks/${id}`);
      return task.status === 200 ? await task.json() : {};
    },

  },

}
</script>
