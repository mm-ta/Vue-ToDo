<template>
  <header>
    <h1>{{ title }}</h1>
    <Button v-show="atHome"
      @btn-clicked="$emit('changeMode')"
      :text="createMode ? 'Cancel' : 'Add Task'" 
      :color="createMode ? 'red' : 'green'"
    />
  </header>
</template>

<script>
  import Button from './Button';

  export default {
    name: 'Header',
    props: {
      title: String,
      createMode: Boolean,
    },
    computed: {
      atHome() {
        if (this.$route.path === '/') {
          return true
        }
        return false;
      }
    },
    components: {
      Button,
    },
    emits: ['changeMode']
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