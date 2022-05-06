<template>
  <header class="nightMode">
    <div class="title">YourChords</div>
    <div class="about">About</div>
  </header>
</template>


<script>

</script>


<style scoped>
header {
  float: left;
  width: 100vw;
  border-bottom: 1px solid;
  border-color: #222;
}
.title {
  float: left;
  font-size: 1.4em;
  color: #eee;
  padding: 10px;
}
.about {
  transition: all .3s;
  cursor: pointer;
  padding: 10px;
  float: right;
  color: #eee;
  opacity: 0.6;
}
.about:hover {
  opacity: 1;
}
</style>
