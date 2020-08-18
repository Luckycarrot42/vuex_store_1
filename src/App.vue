<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <p v-text="busy"></p>
    <p v-text="sale_record"></p>
    <input type="text" placeholder="buscar" v-model="search" />
    <ul v-if="searchById">
      <li>{{ searchById.nombre }}</li>
    </ul>
    <ul>
      <li v-for="(product, index) in availableProducts" :key="index">{{ product.nombre }}</li>
    </ul>
    <h3>Ofertas de último minuto</h3>
    <ul>
      <li v-for="(product, index) in cheapProducts" :key="index">{{ product.nombre }} - {{ product.precio }}</li>
    </ul>
  </div>
</template>

<script>
import {mapState, mapGetters} from "vuex";

export default {
  name: 'App',
  data (){
    return {
      search: null
    }
  },
  computed: {
    ...mapState (["isBusy", "sales"]),  //helper de vuex, importarlo para acceder a var de state mas facilmente
    ...mapGetters (["availableProducts", "cheapProducts", "getProductById"]), //agregar getters in store.js para acarrear informacion
    busy(){
      let statusBusy = this.isBusy ? 'Ocupado' : 'Disponible'
      return `Estado ${statusBusy}`
    },
    sale_record(){
      return `Total de ventas es ${this.sales}`
      // $ interno refiere a plugin
    },
    searchById (){
      return this.getProductById(this.search)
    }
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
ul{
  list-style-type: none;
}
</style>
