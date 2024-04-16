<template>
<div class="container">
    <HeaderComponent @toggle-add-task="toggleAddTask" title="Web Go" :showAddTask="showAddTask" />
    <TasksComponent @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks" />
    <div v-show="showAddTask">
        <AddTaskComponent @add-task="addTask" />

    </div>
</div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue'
import TasksComponent from './components/TasksComponent.vue'
import AddTaskComponent from './components/AddTaskComponent.vue'

export default {
    name: 'App',
    components: {

        HeaderComponent,
        TasksComponent,
        AddTaskComponent
    },
    data() {
        return {
            tasks: [],
            showAddTask: false
        }
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
            console.log("data====", data);
            this.tasks = [...this.tasks, data];
        },


        deleteTask(id) {
            if (confirm('Are you sure ?')) {
                this.tasks = this.tasks.filter((task) => task.id !== id);
            }
        },

        toggleReminder(id) {
            console.log(id);
            this.tasks = this.tasks.map((task) => {
                if (task.id === id) {
                    task.reminder = !task.reminder;
                }
                return task;
            })
        },
        toggleAddTask() {
            this.showAddTask = !this.showAddTask
        },

        async fetchTasks() {
            const res = await fetch('api/tasks');
            console.log("res===========", res);
            const data = await res.json();
            return data;
        }
    },

    async created() {
        this.tasks = await this.fetchTasks();
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: 'Poppins', sans-serif;
}

.container {
    max-width: 500px;
    margin: 30px auto;
    overflow: auto;
    min-height: 300px;
    border: 1px solid steelblue;
    padding: 30px;
    border-radius: 5px;
}

.btn {
    display: inline-block;
    background: #000;
    color: #fff;
    border: none;
    padding: 10px 20px;
    margin: 5px;
    border-radius: 5px;
    cursor: pointer;
    text-decoration: none;
    font-size: 15px;
    font-family: inherit;
}

.btn:focus {
    outline: none;
}

.btn:active {
    transform: scale(0.98);
}

.btn-block {
    display: block;
    width: 100%;
}
</style>
