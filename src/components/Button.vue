<template>
  <button 
    @click="$emit('btn-clicked')" 
    :style="{ background: color }" 
    class="btn">
    {{ text }}
  </button>
</template>

<script>
  export default {
    name: 'Button',
    props: {
      text: String,
      color: String
    },
    emits: ['btn-clicked']
  }
</script>