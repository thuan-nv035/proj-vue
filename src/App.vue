<template>
    <div id="app">
        <div class="medium-4  columns">
            <div class="cart">
                <h1>Cart items</h1>
                <div class="row">
                    <div class="medium-6 columns">
                        <button class="tiny secondary" id="clear">Clear the cart</button>
                    </div>
                    <div class="medium-6 columns">
                        <button class="tiny disabled" title="Work in progress">Checkout</button>
                    </div>
                </div>
                <div id="cartItems" v-for="(cart, index) in carts" :key="index">
                    <div class="product-item ">
                        <div class="thumb">
                            <img :src="cart.thumb" alt="">
                        </div>
                        <h3 class="name">{{cart.name}}</h3>
                        <p class="desc">{{cart.description}}</p>
                        <div class="quantity">
                            <div @click="increaseQuantity(quantity)">
                                -
                            </div>
                            <div>
                                {{quantity}}
                            </div>
                            <div @click="decreaseQuantity(quantity)>
                            +
                            </div>
                        </div>
                    </div>
                </div>
                        <h1 class=" price
                            ">{{cart.price}}</h1>
                            <button class="clear" @click="remove(cart.id)">Remove</button>
                        </div>
                    </div>
                    <div>Total price: <strong id="totalPrice">{{payment()}}</strong></div>
                    <div>VAT: <strong id="">8%</strong></div>
                    <div>Payment: <strong id=""></strong></div>
                </div>
            </div>
            <div class="medium-8 columns">
                <div class="product medium-4 columns" v-for="(item, index) in products" :key="index">
                    <div class="product-item ">
                        <div class="thumb">
                            <img :src="item.thumb" alt="">
                        </div>
                        <h3 class="name">{{item.name}}</h3>
                        <p class="desc">{{item.description}}</p>
                        <h1 class="price">{{item.price}}</h1>
                        <button class="addToCart" @click="addToCart(item.id)">Add to Cart</button>
                    </div>
                </div>
            </div>
        </div>
</template>

<script>
    // import HelloWorld from './components/HelloWorld.vue'

    export default {
        name: 'App',
        components: {},
        data() {
            return {
                products: [],
                carts: [],
                total: 0,
                quantity: 1
            }
        },

        mounted() {
            fetch("https://6246a3c3e3450d61b000fdf0.mockapi.io/products",
                {
                    method: 'GET',
                    headers: {
                        'Authorization': 'Basic ' + btoa('login:password')
                    }
                }
            ).then(res => res.json())
                .then((data) => {
                    this.products = data
                })


        },
        methods: {
            addToCart(id) {
                if (this.carts.find(product => product.id === id)) {
                    alert('sản phẩm đã có trong giỏ hàng  !');
                } else {
                    this.carts.push(this.products.find(product => product.id === id));
                    localStorage.setItem('listCart', JSON.stringify(this.carts));
                }
            },

            remove(id) {
                this.carts.splice(this.carts.find(item => item.id === id), 1);
                localStorage.setItem('listCart', JSON.stringify(this.carts));
            },

            increaseQuantity(quantity) {
                return this.quantity++
            },
            decreaseQuantity(quantity) {
                return this.quantity--
            },

        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        /*text-align: center;*/
        color: #2c3e50;
        margin-top: 60px;
        margin-left: 30px;
    }

    img {
        width: 300px;
        height: 300px;
    }
</style>
