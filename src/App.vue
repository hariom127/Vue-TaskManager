<template>
<div class="container">
    <HeaderComponent title="Web Go" />
    <TasksComponentVue @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks" />
</div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue'
import TasksComponentVue from './components/TasksComponent.vue'

export default {
    name: 'App',
    components: {

        HeaderComponent,
        TasksComponentVue
    },
    data() {
        return {
            tasks: []
        }
    },

    methods: {
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
        }
    },

    created() {
        this.tasks = [{
                "id": 1,
                "todo": "Do something nice for someone I care about",
                "reminder": true,
                "userId": 26
            },
            {
                "id": 2,
                "todo": "Memorize the fifty states and their capitals",
                "reminder": false,
                "userId": 48
            },
            {
                "id": 3,
                "todo": "Watch a classic movie",
                "reminder": false,
                "userId": 4
            },
            {
                "id": 4,
                "todo": "Contribute code or a monetary donation to an open-source software project",
                "reminder": false,
                "userId": 48
            },
            {
                "id": 5,
                "todo": "Solve a Rubik's cube",
                "reminder": false,
                "userId": 31
            },
            {
                "id": 6,
                "todo": "Bake pastries for me and neighbor",
                "reminder": false,
                "userId": 39
            },
            {
                "id": 7,
                "todo": "Go see a Broadway production",
                "reminder": false,
                "userId": 32
            },
            {
                "id": 8,
                "todo": "Write a thank you letter to an influential person in my life",
                "reminder": true,
                "userId": 13
            },
            {
                "id": 9,
                "todo": "Invite some friends over for a game night",
                "reminder": false,
                "userId": 47
            },
            {
                "id": 10,
                "todo": "Have a football scrimmage with some friends",
                "reminder": false,
                "userId": 19
            }
        ]
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
