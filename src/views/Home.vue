<template>
  <div>
    <AddTask v-show="mode" @add-task="addTask" />
    <Tasks @toggle-reminder="toggleReminder" @delete-task="onDelete" :tasks="tasks" />
  </div>
</template>

<script>
  import Tasks from '../components/Tasks';
  import AddTask from '../components/AddTask'

  export default {
    name: 'Home',
    components: {
      Tasks,
      AddTask,
    },
    data() {
      return {
        tasks: []
      }
    },
    props: {
      mode: Boolean
    },
    methods: {
      async onDelete(id) {
        if (confirm('Are you sure about deleting the task?')) {
          const res = await fetch(`api/tasks/${id}`, {
            method: 'DELETE'
          })

          res.status === 200 
            ? (this.tasks = this.tasks.filter((task) => task.id !== id))
            : alert('something wrong happened! :(')
        }
      },

      async toggleReminder(id) {
        const theTask = await this.fetchTask(id);
        const updatedTask = {...theTask, reminder: ! theTask.reminder};

        const res = await fetch(`api/tasks/${id}`, {
          method: 'PUT',
          headers: {
            'Content-type': 'application/json'
          },
          body: JSON.stringify(updatedTask)
        });
        
        const data = await res.json();

        this.tasks = this.tasks.map((task) => task.id === id 
        ? {...task, reminder: data.reminder} 
        : {...task});
      },

      async addTask(newTask) {
        const res = await fetch('api/tasks', {
          method: 'POST',
          headers: {
            'Content-type': 'application/json'
          },
          body: JSON.stringify(newTask)
        });

        const data = await res.json();
        
        this.tasks.push(data);
      },

      async fetchTasks() {
        const res = await fetch('api/tasks');
        const data = await res.json();
        
        return data;
      },

      async fetchTask(id) {
        const res = await fetch(`api/tasks/${id}`);
        const data = await res.json();

        return data;
      },
    },
    async created() {
      this.tasks = await this.fetchTasks();
    },
  }
</script>