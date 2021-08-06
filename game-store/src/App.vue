<template>
  <section  id="app" class="container">
  <section class="flex">
    <div id="gamestore">
      <Main @sendToCart="addToCart" /> 
    </div>
    <div id="shopcart">
      <Shop :inCart="productsInCart"/>      
    </div>
  </section>  

  </section>
</template>

<script>
// import Header from './components/Header'
import Main from './components/Main'
import Shop from './components/Shop'
export default {
  name: 'App',
  components: {
    Main,
    Shop   
  },
  computed: {
      productsInCart() {
        return this.$store.state.productsInCart
      }
    },
  methods: {
    addToCart(product) {
      if(!this.productsInCart.some(elem => elem == product)) {
        this.productsInCart.push(product)
      }
    }
  }
}
</script>

<style>
  * {margin: 0; padding: 0;
      box-sizing: border-box;
    }
    body {font-family: 'Open Sans', sans-serif;}
  .container {
    max-width: 1200px;
    margin: auto;
  }
  #app {
    padding: 50px 0;
  } 
  .flex {
    display: flex;
  }
  #gamestore {
    flex: 1;
  }
  #shopcart {
    margin-left: 30px;
    width: 260px;
  }
</style>
