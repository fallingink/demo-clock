<script setup lang="ts">
import Clock from './components/Clock.vue';
</script>

<template>
 <div :class="$style.center">
  <Clock />
 </div>
</template>

<style module>
.center {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 10vh;
}
</style>
