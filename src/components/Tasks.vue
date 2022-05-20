<template>
  <div 
    v-for="task in tasks"
    :key="task.id">
    <Task @delete-task="$emit('deleteTask', task.id)" :task="task" />
  </div>
</template>

<script>
  import Task from './Task'

  export default {
    name: 'Tasks',
    props: {
      tasks: Array
    },
    components: {
      Task
    },
    emits: ['deleteTask']
  }
</script>