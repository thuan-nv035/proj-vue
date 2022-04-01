<template>
    <div id="app">
        <div class="wrapper">
            <div class="content" v-for="(item, index) in products" :key="index">
                <div class="thumb">
                    <img :src="item.thumb" alt="">
                </div>
                <div class="name">{{item.name}}</div>
                <div class="desc">{{item.description}}</div>
                <div class="price">{{item.price}}</div>
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
                valueInput: "",
                url: `https://6246a3c3e3450d61b000fdf0.mockapi.io/products`,
                options: {method: 'GET'},
            }
        },
        method: {
            api() {
                fetch(this.url).then((res) => {
                    return res.json()
                }).then((data) => {
                    this.products = data
                }).catch((err) => console.log(err))
            }
        },
        mounted() {
            this.api()
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
