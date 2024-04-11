<template>
<button @click="onClick()" :style="{background: color}"   class="btn">{{ title }}</button>    
</template>

<script>

export default {
    name: 'ButtonComponent',
    
    props: {
        title: String,
     color: String
    },
    methods: {
        onClick() {
            console.log("Hi")
        }
    }
}



</script>

