<template>
    <li>
        <p>{{ item.product.brand }} {{ item.product.name }}</p>
        <p>{{ item.product.color }}</p>
        <p>{{ item.product.price }}</p>
        <button v-on:click="remove">Remove</button>
        <label>
            <select name="quantity" v-model.number="newQuantity" v-on:change="changeQuantity" >
                <option
                    v-for="i in Array.from(Array(9).keys())"
                    :key="i"
                    :value="i"
                >
                    {{i === 0 ? `${i} (Remove)` : i}}
                </option>
            </select>
        </label>

        <!--
        The following code allow to do what's done in the above but without using computed property but only a data newQuantity
        <label>
            <select name="quantity" v-on:change="changeQuantity" >
                <option
                        v-for="i in Array.from(Array(9).keys())"
                        :key="i"
                        :value="i"
                        :selected="i === item.quantity"
                >
                    {{i === 0 ? `${i} (Remove)` : i}}
                </option>
            </select>
        </label>
        -->
    </li>
</template>

<script>
  export default {
    name: 'CartItem',
    props: {
      item: {type: Object},
      onRemove: {type: Function},
      onChangeQuantity: {type: Function}
    },
    watch: {
      newQuantity(val) {
        this.newQuantity = val
      }
    },
    methods: {
      remove() {
        this.onRemove(this.item.product.id)
      },
      changeQuantity() {
        this.onChangeQuantity(this.item.product.id, this.newQuantity)
      }
    },
    computed: {
      newQuantity: {
        get() {
          return this.item.quantity
        },
        set(val) {
          this.item.quantity = val
        }
      }
    }
  }
</script>

<style scoped>

</style>
