<template>
  <HeaderComp/>
  <ControlPanel
    v-bind:currentChord="currentChord"
    v-on:changeTone="changeTone"
    v-on:changeAccidentals="changeAccidentals"
    v-on:changeMinor="changeMinor"
    v-on:changeChord="changeChord"
  />
  <Instruments
    v-bind:currentChord="currentChord"
  />
</template>

<script>
import HeaderComp from './components/HeaderComp.vue'
import ControlPanel from './components/ControlPanel.vue'
import Instruments from './components/Instruments.vue'

export default {
  name: "app",
  components: {
    HeaderComp,
    ControlPanel,
    Instruments
  },
  props: {},
  data() {
    return {
      currentChord: {tone: "G", accidental: "#", minor: true, chord: "sus2"}
    }
  },
  methods: {
    changeTone(param) {
      this.currentChord.tone = param
    },

    changeAccidentals(param) {
      if (this.currentChord.accidental == param) {
        this.currentChord.accidental = ''
      } else {
        this.currentChord.accidental = param
      }
    },
    changeMinor(param) {
      if (this.currentChord.minor) {
        this.currentChord.minor = false
      } else {
        this.currentChord.minor = true
      }
    },
    changeChord(param) {
      this.currentChord.chord = param
    },
  },
  computed: {}
}

</script>
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
