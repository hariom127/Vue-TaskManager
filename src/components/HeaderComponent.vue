<template>
<header>
    <h1>{{title}}</h1>
    <ButtonComponent title="Login" color="green" />
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
        }
        // props: ['title']
        // props: {
        //  title: string
        // }
    },
    components: {
        ButtonComponent
    }
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
