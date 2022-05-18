<template>
  <div class="main nightMode">
    <div class="block">
      <div class="title">Основной тон</div>
      <div class="ButtonsGroup">
        <div class="row">
          <button type="button" class="button nightMode cell"
          v-for="n in notes.tones"
          :class="{'active':n==this.currentChord.tone}"
          @click="changeTone(n)"
          >{{n}}</button>

          <div class="sep"></div>

          <button type="button" class="button nightMode cell"
          v-for="n in notes.accidentals"
          :class="{'active':n==this.currentChord.accidental}"
          @click="changeAccidentals(n)"
          >{{n}}</button>

        </div>
      </div>
    </div>
    <div class="block">
      <div class="title">Аккорд</div>
      <div class="ButtonsGroup">
        <div class="cell">
          <div class="vertical">
            <button type="button" class="button nightMode"
            v-for="n in chords.minor"
            :class="{'active':this.currentChord.minor}"
            @click="changeMinor(n)"
            >{{n}}</button>
          </div>
        </div>
        <div class="cell">
          <div class="vertical"><button type="button" class="button nightMode"
            v-for="n in chords.step2"
            :class="{'active':n==this.currentChord.chord}"
            @click="changeChord(n)"
            >{{n}}</button>
          </div>
        </div>
        <div class="cell">
          <div class="vertical"><button type="button" class="button nightMode"
            v-for="n in chords.step4[0]"
            :class="{'active':n==this.currentChord.chord}"
            @click="changeChord(n)"
            >{{n}}</button>
          </div>
        </div>
        <div class="cell">
          <div class="vertical"><button type="button" class="button nightMode"
            v-for="n in chords.step4[1]"
            :class="{'active':n==this.currentChord.chord}"
            @click="changeChord(n)"
            >{{n}}</button>
          </div>
        </div>
        <div class="cell">
          <div class="vertical">
            <div class="horizontal">
              <button type="button" class="button nightMode wider43"
              v-for="n in chords.step5[0]"
              :class="{'active':n==this.currentChord.chord}"
              @click="changeChord(n)"
              >{{n}}</button>
            </div>
            <button type="button" class="button nightMode"
            v-for="n in chords.step5[1]"
            :class="{'active':n==this.currentChord.chord}"
            @click="changeChord(n)"
            >{{n}}</button>
          </div>
        </div>
        <div class="cell">
          <div class="vertical"><button type="button" class="button nightMode"
            v-for="n in chords.step6"
            :class="{'active':n==this.currentChord.chord}"
            @click="changeChord(n)"
            >{{n}}</button>
          </div>
        </div>
        <div class="cell">
          <div class="vertical">
            <div>
              <button type="button" class="button nightMode"
              v-for="n in chords.step7[0]"
              :class="{'active':n==this.currentChord.chord}"
              @click="changeChord(n)"
              >{{n}}</button>
            </div>
            <button type="button" class="button nightMode"
            v-for="n in chords.step7[1]"
            :class="{'active':n==this.currentChord.chord}"
            @click="changeChord(n)"
            >{{n}}</button>
          </div>
        </div>
        <div class="cell">
          <div class="vertical">
            <div class="horizontal">
              <button type="button" class="button nightMode wider44"
              v-for="n in chords.step9[0]"
              :class="{'active':n==this.currentChord.chord}"
              @click="changeChord(n)"
              >{{n}}</button>
            </div>
            <div>
              <button type="button" class="button nightMode"
              v-for="n in chords.step9[1]"
              :class="{'active':n==this.currentChord.chord}"
              @click="changeChord(n)"
              >{{n}}</button>
            </div>
          </div>
        </div>
        <div class="cell">
          <div class="vertical">
            <div>
              <button type="button" class="button nightMode"
              v-for="n in chords.step11[0]"
              :class="{'active':n==this.currentChord.chord}"
              @click="changeChord(n)"
              >{{n}}</button>
            </div>
            <button type="button" class="button nightMode"
            v-for="n in chords.step11[1]"
            :class="{'active':n==this.currentChord.chord}"
            @click="changeChord(n)"
            >{{n}}</button>
          </div>
        </div>
        <div class="cell">
          <div class="vertical">
            <button type="button" class="button nightMode"
            v-for="n in chords.step13"
            :class="{'active':n==this.currentChord.chord}"
            @click="changeChord(n)"
            >{{n}}</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "control",
  components: {},
  props: {
    currentChord: {}
  },
  data() {
    return {
      state: false,
      notes : {
        tones: ['C','D','E','F','G','A','B'],
        accidentals: ['#','♭']
      },
      chords : {
        minor: ["m"],
        step2: ["add2","sus2"],
        step4: [["add4","sus4"],["add#4","sus#4"]],
        step5: [["5","-5"],["5+ / aug"]],
        step6: ["6","6-"],
        step7: [["7","dim7"],["maj7"]],
        step9: [["9","-9"],["maj9","9+"]],
        step11: [["11","11+"],["maj11"]],
        step13: ["13"]
      },
    }
  },
  methods: {
    changeTone: function(param) {
      this.$emit('changeTone', param);
    },
    changeAccidentals: function(param) {
      this.$emit('changeAccidentals', param);
    },
    changeMinor: function(param) {
      this.$emit('changeMinor', param);
    },
    changeChord: function(param) {
      this.$emit('changeChord', param);
    },
  },
  computed: {}
}
</script>


<style scoped>
.main{
  float: left;
  width: 100vw;
  text-align: center;
}
.block {
  width: 100vw;
  overflow: hidden;
  margin: 0 auto;
}
.title {
  text-align: center;
  margin: 10px;
}
.ButtonsGroup {
  justify-content: center;
  margin: 10px auto;
  overflow: hidden;
  text-align: center;
  display: table;
}
.row {
  display: flex
}
@media screen and (orientation: portrait){
  .row {float: none;}}
.vertical {
  display: flex;
  flex-direction: column;
  margin: 3px;
}
.horizontal {
  display: flex;
  flex-direction: row;
}
.cell {
  display: table-cell;
  text-align: center;
  vertical-align: middle;
  text-align: center;
  float: left;
}
.button {
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
.sep {
  float: left;
  margin: 7px 5px 7px 4px;
  border-right: 1.5px solid #ffffff;
}
.active {
  background: #eee;
  color: #222;
}
.button:hover{
  background: rgba(255,255,255,0.1);
}
.active:hover{
  background: rgba(255,255,255,0.7);
}
.wider43 {
  min-width: 43%;
}
.wider44 {
  min-width: 44%;
}
</style>
