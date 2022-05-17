<template>
  <HeaderComp/>
  <ControlPanel
    :currentChord="currentChord"
    @changeTone="changeTone"
    @changeAccidentals="changeAccidentals"
    @changeMinor="changeMinor"
    @changeChord="changeChord"
  />
  <Instruments
    :currentChord="currentChord"
    :stepsInChord="stepsInChord"
    :notesInChord="notesInChord"
    :allNotes="allNotes"
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
      currentChord: {tone: "C", accidental: "", minor: false, chord: ""},
      newArray: '',
      notes: ["C","D","E","F","G","A","B"],
      allNotes: ["C","C#/D♭","D","D#/E♭","E","F","F#/G♭","G","G#/A♭","A","A#/B♭","B"],
      tones: [0,2,4,5,7,9,11],
      stepsInChord: [],
      notesInChord: [],
    }
  },
  created() {
    this.newFunc()
  },

  methods: {
    newFunc(){
      for (var i = 0; i < this.notes.length; i++) {
        switch (this.currentChord.tone) {
          case this.notes[i]:
          var stepTone = this.tones[i];
          if (this.currentChord.accidental=="#") {
            stepTone++};
          if (this.currentChord.accidental=="♭") {
            stepTone--};
            stepTone = this.correctTone(stepTone);
            this.stepsInChord[0] = stepTone;
          break;
        }
      }
// Минорный аккорд
      if (this.currentChord.minor) {
        this.stepsInChord[1] = 3 + stepTone
      } else {this.stepsInChord[1] = 4 + stepTone}
      this.stepsInChord[1] = this.correctTone(this.stepsInChord[1]);
// Мажор
      if (this.currentChord.chord == "") {
        this.stepsInChord[2] = 7 + stepTone;
        this.stepsInChord[2] = this.correctTone(this.stepsInChord[2]);
      }
      for (var i = 0; i < this.stepsInChord.length; i++) {
        this.notesInChord[i] = this.allNotes[this.stepsInChord[i]]
      }
    },
    correctTone(param) {
      if (param<0) {
        param=param+12};
      if (param>=12) {
        param=param-12};
        return param
    },
    changeTone(param) {
      this.currentChord.tone = param
      this.newFunc()
    },

    changeAccidentals(param) {
      if (this.currentChord.accidental == param) {
        this.currentChord.accidental = ''
      } else {
        this.currentChord.accidental = param
      }
      this.newFunc()
    },
    changeMinor(param) {
      if (this.currentChord.minor) {
        this.currentChord.minor = false
      } else {
        this.currentChord.minor = true
      };
      if (this.currentChord.chord == "sus2"
       || this.currentChord.chord == "sus4"
       || this.currentChord.chord == "sus#4"
       || this.currentChord.chord == "5"
       || this.currentChord.chord == "dim7"
          )
        this.currentChord.chord = ''
      this.newFunc()
    },
    changeChord(param) {
      if (this.currentChord.chord == param) {
        this.currentChord.chord = ''
      } else {
        this.currentChord.chord = param
      };
      if (this.currentChord.chord == "sus2"
       || this.currentChord.chord == "sus4"
       || this.currentChord.chord == "sus#4"
       || this.currentChord.chord == "5"
       || this.currentChord.chord == "dim7"
          )
        this.currentChord.minor = false
      this.newFunc()
    },
  },
  computed: {}
}

</script>
<style>
body {
  margin: 0;
  padding: 0;
  /* overflow:hidden; */
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
