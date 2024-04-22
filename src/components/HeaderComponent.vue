<template>
    <header>
        <h1>{{ title }}</h1>
        <ButtonComponent v-show="homePage" @btnClick="$emit('toggle-add-task')"
            :title="showAddTask ? 'Close' : 'Add Task'" :color="showAddTask ? 'red' : 'green'" />
    </header>
</template>

<script>
import ButtonComponent from './ButtonComponent.vue'

export default {
    name: 'HeaderComponent',
    props: {
        title: {
            type: String,
            default: "Go with Vue"
        },
        showAddTask: Boolean
        // props: ['title']
        // props: {
        //  title: string
        // }
    },
    components: {
        ButtonComponent
    },
    computed: {
        homePage() {
            return this.$route.path === '/'
        }
    },
}
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>
