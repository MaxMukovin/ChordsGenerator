<template>
  <div class="instruments">
    <div class="buttonsGroup">
      <button type="button" class="button"
      :class="{'active':this.currentInst=='Piano'}"
      @click="changeInst('Piano')"
      >Пианино</button>

      <button type="button" class="button"
      :class="{'active':this.currentInst=='Guitar'}"
      @click="changeInst('Guitar')"
      >Гитара</button>
    </div>
    <Piano
    v-if="this.currentInst=='Piano'"
    :stepsInChord="stepsInChord"
    :notesInChord="notesInChord"
    :allNotes="allNotes"
    />
    <Guitar
    v-if="this.currentInst=='Guitar'"
    :notesInChord="notesInChord"
    />
  </div>
  <div class="chord">
    <p>{{textChord}}</p>
    <!-- <p>{{stepsInChord}}</p>
    <p>{{notesInChord}}</p> -->
  </div>
</template>


<script>
import Piano from './Piano.vue'
import Guitar from './Guitar.vue'

export default {
  name: "instrument",
  components: {
    Piano,
    Guitar,
  },
  props: {
    currentChord: {},
    stepsInChord: {},
    notesInChord: {},
    allNotes: {},
  },
  data() {
    return {
      currentInst: "Piano",
    }
  },
  methods: {
    changeInst: function(param) {
      this.currentInst = param;
    },
  },
  computed: {
// Собираем текстовую запись аккорда
    textChord() {
      var tone = this.currentChord.tone
      var accidental = this.currentChord.accidental
      var minor = this.currentChord.minor
      var chord = this.currentChord.chord

      if (accidental == "0") {
        accidental = "";
      }
      if (minor) {
        minor = "m";
      } else {
        minor = "";
      }
      return `${tone}${accidental}${minor} ${chord}`
    },
  }
}
</script>
<style scoped>

.instruments {
  float: left;
  width: 100%;
}
.buttonsGroup {
  justify-content: center;
  margin: 0 auto;
  overflow: hidden;
  text-align: center;
  display: flex;
  margin: 10px;
}
.button {
  background: none;
  float: left;
  font-size: 1.1em;
  transition: all .3s;
  color: inherit;
  outline: none;
  border: 1.5px solid;
  border-color: #eee;
  cursor: pointer;
  border-radius: 5px;
  margin: 3px;
  padding: 7px;
  min-width: 29px;
}
.active {
  background: #eee;
  color: #222;
}
.chord {
  font-size: 2em;
  float: left;
  width: 100%;
  text-align: center;
  vertical-align:middle;
  display:table-cell;
}
</style>
