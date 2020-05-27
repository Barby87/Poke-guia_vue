<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="text" v-model="texto">
    <p>{{info}}</p>
    <p>----------------</p>
    <p>Mensaje original: {{titulo}}</p>
    <p>Mensaje nuevo:{{reverso}}</p>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
  data() {
    return {
      texto: '',
      info: null,
      titulo: 'VueJS desde componente'
    }
  },
  props: {
    msg: String
  },
  computed: {
    reverso() {
      return this.titulo.split('').reverse().join('');
    }
  },
  methods: {
    moneda(){
      axios
      .get('https://api.coindesk.com/v1/bpi/currentprice.json')
      .then(response => {
        console.log(response)
        this.info = response
        });
    }
  },
  // Llamado a una api
  beforeCreate() {
    console.log('beforeCreate desde component')
  },
  created() {
    console.log('created desde component')
  },
  beforeMount() {
    console.log('beforeMount desde component')
  },
  mounted() {
    console.log('mounted desde component')
  },
  beforeUpdate() {
    console.log('beforeUpdate desde component');
    // Llamando a función moneda
    this.moneda();
  },
  updated() {
    console.log('updated desde component')
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
