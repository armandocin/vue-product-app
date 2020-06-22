<template>
  <div id="app">
    <NavBar msg="Welcome to Your Vue.js App"/>
    <Cart :cart="cart" v-on:remove-from-cart="removeFromCart" />
    <Product :product="selectedProduct" v-on:add-to-cart="updateCart" />
  </div>
</template>

<script>
import omit from 'lodash/omit'
import NavBar from './components/Navbar.vue'
import Product from './components/Product.vue'
import Cart from './components/Cart.vue'

import {socks as socksAnnouncements} from './data/annauncements'
import {socks as socksProducts} from './data/socks-products'

export default {
  name: 'App',
  data: () => {
    return {
      selectedProduct: {
        ...socksAnnouncements[0],
        variants: socksAnnouncements[0].variants.map(id => socksProducts.find(p => p.id === id))
      },
      cart: {}
    }
  },
  components: {
    NavBar,
    Product,
    Cart
  },
  methods: {
    updateCart(product) {
      if (this.cart[product.id]) {
        this.cart[product.id].quantity += 1
      } else {
        this.cart = {
          ...this.cart,
          [product.id]: {
            product,
            quantity: 1
          }
        }
      }
    },
    removeFromCart(id, quantity) {
      if (quantity === this.cart[id].quantity) {
        this.cart = omit(this.cart, id)
      } else {
        this.cart[id].quantity -= quantity
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

h3 {
  margin: 40px 0 0;
}
a {
  color: #42b983;
  cursor: pointer;
}

button {
  display: block;
  margin-top: 30px;
  border: none;
  background-color: #1E95EA;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
  cursor: pointer;
}

.button-disabled {
  background-color: #d8d8d8;
  cursor: default;
}

</style>
