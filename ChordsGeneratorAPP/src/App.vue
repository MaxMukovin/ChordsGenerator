<script setup>
import HeaderComp from './components/HeaderComp.vue'
import ControlPanel from './components/ControlPanel.vue'
import Instruments from './components/Instruments.vue'
</script>

<template>
  <HeaderComp/>
  <ControlPanel/>
  <Instruments/>
</template>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
  color: #eee;
  background: #191E22;
}
.dayMode {

}
.nightMode {
  background: #2B445D;
}
</style>
