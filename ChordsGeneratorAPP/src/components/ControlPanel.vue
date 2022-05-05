<template>
  <div class="main nightMode">
    <div class="Title">Основной тон</div>
    <div class="ButtonsGroup">
      <button type="button" class="button nightMode"
      v-for="n in notes.tones">{{n}}</button>
      <div class="sep"></div>
      <button type="button" class="button nightMode"
      v-for="n in notes.accidentals">{{n}}</button>
    </div>
    <div class="Title">Аккорд</div>

    <div class="ButtonsGroup">
<!-- Минорный аккорд -->
      <div class="vertical">
        <button type="button" class="button nightMode"
        v-for="n in chords.minor">{{n}}</button>
      </div>
<!-- Ступень 2 -->
      <div class="vertical"><button type="button" class="button nightMode"
        v-for="n in chords.step2">{{n}}</button>
      </div>
<!-- Ступень 4 -->
      <div class="vertical"><button type="button" class="button nightMode"
        v-for="n in chords.step4[0]">{{n}}</button>
      </div>

      <div class="vertical"><button type="button" class="button nightMode"
        v-for="n in chords.step4[1]">{{n}}</button>
      </div>
<!-- Ступень 5 -->
      <div class="vertical">
        <div class="horizontal">
          <button type="button" class="button nightMode wider43"
          v-for="n in chords.step5[0]">{{n}}</button>
        </div>
        <button type="button" class="button nightMode"
        v-for="n in chords.step5[1]">{{n}}</button>
      </div>
<!-- ступень 6 -->
      <div class="vertical"><button type="button" class="button nightMode"
        v-for="n in chords.step6">{{n}}</button>
      </div>
<!-- Ступень 7 -->
      <div class="vertical">
        <div>
          <button type="button" class="button nightMode"
          v-for="n in chords.step7[0]">{{n}}</button>
        </div>
        <button type="button" class="button nightMode"
        v-for="n in chords.step7[1]">{{n}}</button>
      </div>
<!-- Ступень 9 -->
      <div class="vertical">
        <div class="horizontal">
          <button type="button" class="button nightMode wider44"
          v-for="n in chords.step9[0]">{{n}}</button>
        </div>
        <div>
          <button type="button" class="button nightMode"
          v-for="n in chords.step9[1]">{{n}}</button>
        </div>
      </div>
<!-- Ступень 11 -->
      <div class="vertical">
        <div>
          <button type="button" class="button nightMode"
          v-for="n in chords.step11[0]">{{n}}</button>
        </div>
        <button type="button" class="button nightMode"
        v-for="n in chords.step11[1]">{{n}}</button>
      </div>
<!-- Ступень 13 -->
      <div class="vertical">
        <button type="button" class="button nightMode"
        v-for="n in chords.step13">{{n}}</button>
      </div>


    </div>
  </div>
</template>


<script setup>
  var notes = {
    tones: ['C','D','E','F','G','A','B'],
    accidentals: ['#','♭']
  };
  var chords = {
    minor: ["m"],
    step2: ["add2","sus2"],
    step4: [["add4","sus4"],["add#4","sus#4"]],
    step5: [["5","-5"],["5+ / aug"]],
    step6: ["6","6-"],
    step7: [["7","dim7"],["maj7"]],
    step9: [["9","-9"],["maj9","9+"]],
    step11: [["11","11+"],["maj11"]],
    step13: ["13"]
  }
</script>


<style scoped>
.main{
  float: left;
  width: 100%;
  text-align: center;
  vertical-align:middle;
  display:table-cell;
}
.Title {
  padding: 10px;
}
.ButtonsGroup {
  display: flex;
  justify-content: center;
  margin-bottom: 7px;
}
.sep {
  border-right: 1.5px solid #ffffff;
  margin: 7px 5px 7px 4px;

}
.button {
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
.button:hover{
  background: rgba(255,255,255,0.1);
}
.vertical {
  display: flex;
  flex-direction: column;
  margin: 3px;
}
.horizontal {
  display: flex;
  flex-direction: row;
}
.wider43 {
  min-width: 43%;
}
.wider44 {
  min-width: 44%;
}
</style>
