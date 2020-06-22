<template>
    <li>
        <p>{{ item.product.brand }} {{ item.product.name }}</p>
        <p>{{ item.product.color }}</p>
        <p>{{ item.product.price }}</p>
        <p>Quantity: {{ item.quantity }}</p>
        <form v-on:submit.prevent="remove">
            <div class="form-remove-item">
                <input type="submit" value="Remove">
                <input id="quantity" v-model.number="quantityToRemove">
            </div>
        </form>
    </li>
</template>

<script>
  export default {
    name: 'CartItem',
    props: {
      item: {type: Object},
      onRemove: {type: Function}
    },
    data() {
      return {
        quantityToRemove: this.item.quantity
      }
    },
    watch: {
      item(i) {
        this.quantityToRemove = i.quantity
      }
    },
    methods: {
      remove() {
        this.onRemove(this.item.product.id, this.quantityToRemove)
      }
    }
  }
</script>

<style scoped>

</style>
