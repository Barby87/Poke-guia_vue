<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <br>
    <input type="text" v-model="texto" @key.enter="mostrar">
    <p>{{info}}</p>
    <hr>
    <p>El resultado es: {{contando}}</p>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data() {
    return {
      texto: '',
      info: null
    }
  },
  components: {
    HelloWorld
  },
  computed: {
    // Las propiedades computadas consumen más recursos que los métodos , ya que siempre están retornando un valor calculado en base e una variable
    contando() {
      return this.texto.length;
    }
  },
  methods: {
    mostrar() {
      alert(`Ingresaste: ${this.texto}`)
    }
  },
  beforeCreate() {
    console.log('beforeCreate desde App');
    this.moneda()
  },
  created() {
    console.log('created desde App')
  },
  beforeMount() {
    console.log('beforeMount desde App')
  },
  mounted() {
    console.log('mounted desde App')
    fetch('https://jsonplaceholder.typicode.com/todos/1')
      .then(response => response.json())
      .then(json => {
        console.log(json)
        this.info = json;
      }); // parses response to JSON
  },
   beforeUpdate() {
    console.log('beforeUpdate desde App')
  },
  updated() {
    console.log('updated desde App')
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
