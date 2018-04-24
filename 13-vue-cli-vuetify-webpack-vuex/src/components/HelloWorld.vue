<template>
  <v-container fluid>
    <v-slide-y-transition mode="out-in">
      <v-layout column align-center>
        <h1>Estado</h1>
        <h2>{{$store.state.number}}</h2>
        <p><button @click="incNumber(2)">Incrementa</button></p>
      </v-layout>
    </v-slide-y-transition>
  </v-container>
</template>
<script>
  import { mapMutations } from 'vuex'
  export default {
    data () {
      return {
        number: 0
      }
    },
    methods:
      mapMutations([
        'incNumber'
      ]),
    name: 'HelloWorld',
    created: function () {
      this.number = this.$store.state.number
      /*
      this.number = this.$store.dispatch('getNumber').then(function (data) {
        return data
      })
      */
    }
  }
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
