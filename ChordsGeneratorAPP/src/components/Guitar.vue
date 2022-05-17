<template>
  <div class="">
    {{notesChord}} <br>
    {{a}} <br>
    {{b}}
  </div>
</template>


<script>
export default {
  props: {
    notesChord: {
      type: Array,
      required: true,
    }
  },
  data() {
    return{
      a: 1,
      b: this.plus()
    }
  },
  methods: {
    plus() {
      var b = this.a*2;
      return b
    }
  },
  created() {
    // this.b[0] = this.a*3
    // this.b[1] = this.a*2
    // console.log(this.b)
  },

  compuded: {

  },
}


</script>


<style>
</style>
