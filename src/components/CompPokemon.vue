<template>
  <div>
      <h1>{{ num }} {{ name | upper }}</h1>
      <small>{{ url }}</small>
    </div>
</template>

<script>
export default {
  name: 'CompPokemon',
  props: {
    name: String,
    url: String,
    num: Number
  },
  filters: {
    upper: function(value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
