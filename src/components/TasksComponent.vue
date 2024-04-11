<template>
 <div :key="task.id" v-for="task in tasks">
    <TaskComponent
    @delete-task="$emit('delete-task', task.id)"
    @toggle-reminder="$emit('toggle-reminder', task.id)"
      :task="task"
    />
  </div>
</template>

<script>

import TaskComponent from './TaskComponent.vue';

export default {
    name: 'TasksComponent',
    props: ['tasks', 'toggle-reminder'],
    components: {
        TaskComponent
  },
  emits: ['delete-task'],
}
</script>
