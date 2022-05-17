<template>
  <div class="main">
    <div class="keyboard">
      <div class="note"
      v-for="n in this.notes.length"
      :class="{mainTone:classMainTone(n, this.notes),chordTone:classChordTone(n, this.notes)}"
      >{{}}</div>
      <div class="sharps">
        <div class="sharp"
        v-for="n in this.sharps.length"
        :class="{mainTone:classMainTone(n, this.sharps),chordTone:classChordTone(n, this.sharps),none:n==3||n==7||n==10}"
        >{{}}</div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: "Piano",
  components: {},
  props: {
    notesInChord: {},
    allNotes: {},
  },
  data() {
    return {
      notes: ["C","D","E","F","G","A","B","C","D","E","F","G","A","B"],
      sharps: ["C#/D♭","D#/E♭","","F#/G♭","G#/A♭","A#/B♭","","C#/D♭","D#/E♭","","F#/G♭","G#/A♭","A#/B♭"],
    }
  },
  methods: {
    classMainTone (param, paramArray) {
      if (this.notesInChord[0]==paramArray[param-1] && param<8 )
        {return true}
      },
    classChordTone (param, paramArray) {
      for (var i = 1; i < this.notesInChord.length; i++) {
        if (this.notes.indexOf(this.notesInChord[0])>=0 // индекс основного тона в массиве
            && this.notesInChord[i]==paramArray[param-1] // нота аккорда == нота в массиве
            && param>this.notes.indexOf(this.notesInChord[0])
            && param<this.notes.indexOf(this.notesInChord[0])+8
        ) {return true} else if (
            this.sharps.indexOf(this.notesInChord[0])>=0
            && this.notesInChord[i]==paramArray[param-1] // нота аккорда == нота в массиве
            && param>this.sharps.indexOf(this.notesInChord[0])
            && param<this.sharps.indexOf(this.notesInChord[0])+8
        ) {return true}
      }
    },
  },
  computed: {},
}

</script>
<style scoped>
.main {
  justify-content: center;
  margin: 0 auto;
  overflow: hidden;
  text-align: center;
  display: table;
}
p {color: red}
.keyboard {
  position: relative;
  color: #696969;
  padding: 8px;
  margin: 10px;
  overflow: hidden;
  border: 1px solid #F4F6F8;
  border-radius: 8px;
  float: left;
  text-align: center;
}
.note {
  transition: all .5s;

  float: left;
  height: 150px;
  width: 40px;
  background: #F4F6F8;
  border: 1px solid #363E45;
  border-radius: 0px 0px 5px 5px;
}
.sharps {
  position: absolute;
  margin-left: 18px;
}
.sharp {
  float: left;
  margin-left: 7px;
  height: 100px;
  width: 32.7px;
  background: #363E45;
  border: 1.5px solid;
  border-color: #363E45;
  border-radius: 0px 0px 5px 5px;
}
.none {background: none; border: none;
}
.mainTone {background: #81A6BB;}
.chordTone {background: #95D9FF;}

</style>
