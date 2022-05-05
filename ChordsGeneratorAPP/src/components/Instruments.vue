<template>
  <div class="main">
    <p>Как же я заколебался это всё ровнять...</p>
    <!-- <Piano/> <p>or</p>
    <Guitar/> -->
  </div>
</template>


<script setup>
import Piano from './Piano.vue'
import Guitar from './Guitar.vue'

</script>


<style scoped>
.main{
  float: left;
  height: 63vh;
  width: 100%;
  text-align: center;
  vertical-align:middle;
  display:table-cell;
}

</style>
