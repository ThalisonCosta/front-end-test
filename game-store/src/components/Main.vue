<template>

<section>
    <div id="head"> 
        <h1>Games</h1>
        <!-- <input type="text" value=""> -->
        <select name="order" v-model="order">
            <option value="score">Mais populares</option>
            <option value="lesspop">Menos populares</option>
            <option value="price">Maiores valores</option>
            <option value="smallprice">Menores valores</option>
            <option value="name">Ordem Alfabética</option>
        </select>
    </div>

    <section id="allGames" >
        <div class="game" v-for="game in sortGames(gamesList)" :key="game.id" @click="sendProduct(game)" @mouseover="hover = game.id" @mouseleave="hover = false">
            <div class="image">
                <img :src="require('../assets/' + game.image)">
            </div>
            <div class="add-to" v-if="hover==game.id"> 
                <span v-if="productsInCart.some(product => product.id === game.id)">produto já adicionado</span>
                <span v-else>adicionar ao carrinho</span>
            </div>
            <div v-else>
                <p>{{game.name}}</p>
                <span>{{ 'R$ ' + game.price}}</span>
            </div>
            </div>
    </section>
</section>

</template>

<script>
export default {
    data () {
        return {
            gamesList: [],
            hover: null,
            order: 'score',
        }
  },
  mounted () {
    this.axios.get('https://raw.githubusercontent.com/ConsultaRemedios/frontend-challenge/master/products.json').then((response) => {
      this.gamesList = response.data
    })
  },
  methods: {
      sendProduct(game) {           
          this.$emit('sendToCart', (game));
      },
      sortGames(games){
          if(this.order == 'smallprice') {
              return games.slice().sort((a, b) => a.price - b.price);        
          }
          if(this.order == 'lesspop') {
              return games.slice().sort((a, b) => a.score - b.score);
          }
          if(this.order == 'name') {
              return games.slice().sort(function(a, b){
                  return (a.name > b.name) ? 1 : -1;
              });
          }       
          return games.slice().sort((a, b) => b[this.order] - a[this.order]);
      }
    },
    computed: {
        productsInCart() {
            return this.$store.state.productsInCart 
        }    
    }   
}
</script>

<style scoped>
    #allGames{
        display: flex;
        flex-wrap: wrap;
        text-align: center;
    }
    span{
        color: #3486E6; 
        font-weight: bold;
    }
    .game{
        width: 31.33%;
        cursor: pointer;
    }
    .game .image img{
        width: 100%;
        height: auto;
    }
    .game .image {
        background-color: #eee;
        padding: 25px 40px;
        margin-bottom: 10px;
    }

    .game .add-to {line-height: 44px;}

    .game:nth-child(n + 4) {
        margin-top: 30px;
    }
    div:nth-child(3n + 2){
        margin:0 3%;
    }
    #head {
    display: flex;  
    align-items: center; 
    justify-content: space-between; 
    margin-bottom: 30px;
    }
    #head select {
        text-align: center;
        width: 262px;
        height: 40px;
        border-radius: 4px;
    }
    #head h1 {
        font-size: 48px;
    }
</style>