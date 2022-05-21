<template>
  <div 
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']">
    <h3>
      {{task.text}}
      <i @click="$emit('deleteTask', task.id)" class="fas fa-times"></i>  
    </h3>
    <p>{{task.time}}</p>
</div>
</template>

<script>
  export default {
    name: 'Task',
    props: {
      task: Object
    }
  }
</script>

<style scoped>
  .fas {
  color: red;
  }
  .task {
    background: #e9e9e9;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
  }
  .task.reminder {
    border-left: 5px solid green;
  }
  .task h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
</style>