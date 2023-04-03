<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <HelloWorld msg="Fake Store" />
  <Products></Products>

 
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
// eslint-disable-next-line no-unused-vars
import Products from './components/products.vue';

export default {
  data() {
    return {
    }
  },
  name: 'App',
  components: {
    HelloWorld,
    Products
}
  // mounted() {
  //   axios.get('https://fakestoreapi.com/products')
  //     .then(response => {
  //       this.productos = response.data;
  //     })
  //     .catch(error => {
  //       console.log(error);
  //     });
  // }
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

body{
  background: rgb(234, 238, 241);
}
</style>
