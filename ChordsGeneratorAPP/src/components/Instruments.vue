<template>
  <div class="chord">
    <p>{{textChord}}</p>
  </div>
</template>


<script>
import Piano from './Piano.vue'
import Guitar from './Guitar.vue'

export default {
  name: "instrument",
  components: {
    Piano,
    Guitar
  },
  props: {
    currentChord: {}
  },
  data() {
    return {
      testData: {
        row1: ["1", "2", "3", "4", "5"],
        row2: ["6", "7", "8", "9", "10"],
      }
    }
  },
  computed: {
    textChord: function () {
      var tone = this.currentChord.tone
      var accidental = this.currentChord.accidental
      var minor = this.currentChord.minor
      var chord = this.currentChord.chord

      if (accidental == "0") {
        accidental = "";
      }
      if (minor == true) {
        minor = "m";
      } else {
        minor = "";
      }
      return `${tone}${accidental}${minor}${chord}`
    }
  }
}

</script>


<style scoped>
.chord {
  font-size: 2em;
  float: left;
  width: 100%;
  text-align: center;
  vertical-align:middle;
  display:table-cell;
}
</style>
