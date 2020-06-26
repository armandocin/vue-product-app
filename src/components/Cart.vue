<template>
    <div class="cart">
        <p>Cart ({{ itemsNUmber }})</p>
        <ul>
            <CartItem
                v-for="(value, key) in cart"
                :key="key"
                :item="value"
                :onRemove="removeFromCart"
                :onChangeQuantity="changeQuantity"
            />
        </ul>
        <p>Total: {{ total }}</p>
    </div>
</template>

<script>
import CartItem from './CartItem'
export default {
  name: 'Cart',
  components: {CartItem},
  props: {
    cart: {type: Object}
  },
  methods: {
    removeFromCart(id) {
      this.$emit('remove-from-cart', id)
    },
    changeQuantity(id, quantity) {
      this.$emit('change-quantity', id, quantity)
    }
  },
  computed: {
    itemsNUmber() {
      return Object.values(this.cart).reduce((acc, item) => acc + item.quantity, 0)
    },
    total() {
      return Object.values(this.cart).reduce((acc, item) => acc + item.quantity*item.product.price, 0)
    }
  }
}
</script>

<style scoped>
.cart {
    margin-right: 25px;
    float: right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
}
</style>
