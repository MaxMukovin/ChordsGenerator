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
      chordsArr: [
        ["",7,'|','|'],
        ['add2',2,7,'|'],
        ['sus2',2,7,'|'],
        ['add4',5,7,'|'],
        ['sus4',5,7,'|'],
        ['add#4',6,7,'|'],
        ['sus#4',6,7,'|'],
        ['5',7,'|'],
        ['5+ / aug',8,'|'],
        ['-5',6,'|'],
        ['6',7,9,'|'],
        ['6-',7,8,'|'],
        ['7',7,10,'|'],
        ['maj7',7,11,'|'],
        ['dim7',3,6,9,'|'],
        ['9',2,7,10,'|'],
        ['maj9',2,7,11,'|'],
        ['-9',1,7,10,'|'],
        ['9+',4,7,10,3,'|'],
        ['11',5,10,'|',2,7],
        ['11+',6,10,'|',2,7],
        ['maj11',5,11,'|',2,7],
        ['13',9,10,'|',2,5,7]
      ]
    }
  },
  created() {

    if (this.readCookie('tone') != undefined ) { //если cookie непустые - читаем
      this.currentChord.tone = this.readCookie('tone');
    
      if (this.readCookie('minor')=='true') {
        this.currentChord.minor = true;
      } else {this.currentChord.minor = false;}
      this.currentChord.chord = this.readCookie('chord');
      if (this.readCookie('accidental') == 'b') {
        this.currentChord.accidental = '♭';
      } else {
        this.currentChord.accidental = this.readCookie('accidental');
      }
    }
    this.createChord(); //создаём аккорд
  },

  methods: {
    writeCookeiCurrentChord() {
      this.writeCookie('tone', this.currentChord.tone, 30);
      this.writeCookie('minor', this.currentChord.minor, 30);
      this.writeCookie('chord', this.currentChord.chord, 30);
      if (this.currentChord.accidental == '♭') {
        this.writeCookie('accidental', 'b', 30);
      } else {
        this.writeCookie('accidental', this.currentChord.accidental, 30);
      }
    },
    writeCookie(name, val, expires) {
      var date = new Date;
      date.setDate(date.getDate() + expires);
      document.cookie = name+"="+val+"; path=/; expires=" + date.toUTCString();
    },
    readCookie(name) {
      var matches = document.cookie.match(new RegExp(
        "(?:^|; )" + name.replace(/([\.$?*|{}\(\)\[\]\\\/\+^])/g, '\\$1') + "=([^;]*)"
      ));
      return matches ? decodeURIComponent(matches[1]) : undefined;
    },
    createChord(){
      this.stepsInChord[0] = this.tones[this.notes.indexOf(this.currentChord.tone)];
      if (this.currentChord.accidental=="#")
      {this.stepsInChord[0]++};
      if (this.currentChord.accidental=="♭")
      {this.stepsInChord[0]--};
      this.stepsInChord[0] = this.correctTone(this.stepsInChord[0]);
// Минорный аккорд
      if (this.currentChord.minor) {
        this.stepsInChord[1] = 3 + this.stepsInChord[0]
      } else {this.stepsInChord[1] = 4 + this.stepsInChord[0]}
      this.stepsInChord[1] = this.correctTone(this.stepsInChord[1]);
// Строим аккорд
      for (var i = 0; i < this.chordsArr.length; i++) {
        if (this.currentChord.chord == "sus2"
         || this.currentChord.chord == "sus4"
         || this.currentChord.chord == "sus#4"
         || this.currentChord.chord == "5"
         || this.currentChord.chord == "dim7"
         || this.currentChord.chord == "9+"
       ) {this.stepsInChord[1] = ''}
        switch (this.chordsArr[i][0]) {
          case this.currentChord.chord:
          for (var n = 1; n < this.chordsArr[this.chordsArr.length-1].length; n++) {
            if (this.chordsArr[i][n]!='|') {
              this.stepsInChord[n+1] = this.correctTone(this.chordsArr[i][n] + this.stepsInChord[0]);
            } else {this.stepsInChord[n+1] = '|'}
          }
          break;
        }
      }
      for (var i = 0; i < this.stepsInChord.length; i++) {
        this.notesInChord[i] = this.allNotes[this.stepsInChord[i]]
      }
      this.writeCookeiCurrentChord();
    },
    correctTone(param) { // Корректируем тон
      if (param<0) {param=param+12};
      if (param>=12) {param=param-12};
      return param
    },
    changeTone(param) {
      this.currentChord.tone = param
      this.createChord()
    },

    changeAccidentals(param) {
      if (this.currentChord.accidental == param) {
        this.currentChord.accidental = ''
      } else {
        this.currentChord.accidental = param
      }
      this.createChord()
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
       || this.currentChord.chord == "9+"
          )
        this.currentChord.chord = ''
      this.createChord()
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
      this.createChord()
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
