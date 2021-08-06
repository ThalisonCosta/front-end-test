<template>
    <div id="shop">

        <div class="container">
            <div id="quant-prod">
                <h2>Carrinho</h2>
                <p v-if="inCart.length"> ({{ inCart.length > 1 ? inCart.length + ' itens' : inCart.length + ' item' }}) </p>
            </div>
        </div>

        <div v-if="!inCart.length" id="cart-txt" class="container">
            <img :src="require('../assets/cart-icon.svg')">
            <p>Até o momento, o seu carrinho está vazio.</p>
        </div>

        <div v-else class="container">
            <div class="cart" v-for="(game, index) in inCart" :key="game.id">
                <div class="cart-img">
                    <img :src="require('../assets/' + game.image)">
                </div>
                <div class="prod-infos">
                    <p> {{ game.name }} </p>
                    <span> {{'R$ ' + game.price }} </span>
                </div>
                <a id="removebtn" @click="removeItem(index)">x</a>
            </div>
            <div id="subtotal" class="flex space-bet ">
                <p>subtotal</p>
                <span> {{ 'R$ ' + subtotal(inCart) }} </span>
            </div>
            <div id="frete" class="flex space-bet">
                <p>Frete</p>
                <span v-if="this.subTotal > 250"> Grátis</span>
                <span v-else>{{"R$ " + calcFrete()}} </span>
            </div>
            <div id="total" class=" flex space-bet">
                <p>Total</p>
                <span> {{ "R$ " +  lastTotal()}} </span>
            </div>
            <div>
                <a id="button" href="#"> Finalizar compra</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            frete: null,
            subTotal: null,
            total: null
        }
    },
    props: {
        inCart: {Array}
    },
    methods: {
      removeItem(index) {
          this.inCart.splice(index, 1)
        },
      subtotal(inCart) {
            this.subTotal = 0
            for(var n in inCart){
                this.subTotal += inCart[n].price;
            }
            return this.subTotal.toFixed(2)
        },
        calcFrete() {
            this.frete = 0
            this.frete += this.inCart.length*10
            return this.frete.toFixed(2)
        },
        lastTotal() {
            this.total = 0
            this.total += this.frete + this.subTotal
            if(this.total >= 250) {
                this.frete = 0
            }
            return this.total.toFixed(2)
        }
    },
    // computed: {
    //     inCart() {
    //         return this.$store.state.inCart
    //     }
    // }
}
</script>   

<style scoped>
    .container {
        margin: 0 20px;
    } 
    .flex {
        display: flex;
    }
    #shop {
        width: 260px;
        border: 1px solid #E1E1E1;
        min-width: 262px;
        min-height: 325px;
    }
    .space-bet {
        justify-content: space-between;
    }
    #quant-prod {
        display: flex;
    }
    #quant-prod p {
        margin-top: 27px;
        margin-left: 4px; 
    }    
    h2 {
        margin-top: 20px;
    }
    p {
        color: #7F7575;
    }
    span {
        font-weight: bold;
    }
    .cart {
        align-items: center;
        max-width: 222px;
        display: flex;
        margin:20px 0;
        /* justify-content: space-between; */
    }
    .cart img {
        background-color: #eee;
    }
    #removebtn {
        display: block;
        font-size: 12px;
        cursor: pointer;
        text-align: center;
        background: #54A3FF ;
        color: white;
        width: 15px;
        height: 15px;
        line-height: 13px;
        border-radius: 50%;
        flex-shrink: 0;
        opacity: 0;
        transition: 0.3s;
    }

    .cart:hover #removebtn {opacity: 1;}

    img {
        max-width: 70px;
        max-height: 70px;
        padding: 6px 10px;
    }
    .prod-infos {
        max-width: 150px;
        margin-left: 10px;
    }
    #subtotal {
        margin-top: 25px;
        margin-bottom: 18px;
    }
    #total {
        margin-top: 20px;
        margin-bottom: 26px;
    }
    #button {
        border-radius: 3px;
        padding: 15px 43px;
        background-color: #54A3FF;
        color: white;
        text-decoration: none;
        margin-bottom: 13px;
        display: block;
    }
    #cart-txt {
        width: 200px;
        text-align: center;
        margin-top: 55px;
    }
    #cart-txt p{
        height: 38px;
        font: normal normal normal 14px/19px;
        /* margin-top: 18px; */
    }
    #cart-txt img {
        max-width: 90px;
        max-height: 72px;
    }

</style>