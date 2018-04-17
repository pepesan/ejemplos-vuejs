<template>
  <div class="about">
    <h1>{{ msg }}</h1>
    <h2>{{ $route.params.id }}</h2>
    <p><button @click="volver">Volver</button></p>
  </div>
</template>

<script>
export default {
  name: 'OtroComponente',
  data () {
    return {
      msg: 'OtroComponente'
    }
  },
  methods: {
    volver: function () {
      window.history.length > 1 ? this.$router.go(-1) : this.$router.push('/')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }

</style>
