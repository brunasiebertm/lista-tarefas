<script setup>
  defineProps(['nome', 'basic'])
</script>

<template>
  <button :class="[basic]">
    <slot>
      
    </slot>
  </button>
</template>

<style scoped>
.btn {
  color: white;
  background-color: red;
  border-color: red;  
  border-radius: 5px;
  
}
</style>