<template>
  <div class="container-wide">
    <Cart
        :cart="cart"
        v-on:remove-from-cart="removeFromCart"
        v-on:change-quantity="changeQuantity"
    />
    <Product :product="selectedProduct" v-on:add-to-cart="updateCart" />
  </div>
</template>

<script>
  import omit from 'lodash/omit'
  import Product from '../components/Product.vue'
  import Cart from '../components/Cart.vue'

  import {socks as socksAnnouncements} from '../data/annauncements'
  import {socks as socksProducts} from '../data/socks-products'

  export default {
    name: 'Home',
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
      removeFromCart(id) {
        this.cart = omit(this.cart, id)
      },
      changeQuantity(id, quantity) {
        if (quantity === 0) {
          this.cart = omit(this.cart, id)
        } else {
          this.cart[id].quantity = quantity
        }
      }
    }
  }
</script>

<style>

</style>
