<template>
    <div class="product">
        <div class="product-image">
            <img v-bind:src="require(`../assets/${image}.jpg`)" />
        </div>

        <div class="product-info">
            <h1>{{ title }}</h1>
            <!-- v-show is more performant than if-else-->
            <p v-show="this.variants[this.selectedVariant].quantity >= 10">In Stock</p>
            <p v-show="this.variants[this.selectedVariant].quantity < 10 && this.variants[this.selectedVariant].quantity > 0">Almost sold out!</p>
            <p v-show="!this.variants[this.selectedVariant].quantity">Out of Stock</p>

            <ul>
                <li :key="detail" v-for="detail in details">{{ detail }}</li>
            </ul>

            <div>
                <div
                    :key="variant.id"
                    v-for="(variant, index) in variants"
                    v-on:mouseover="changeSelectedProduct(index)"
                    :class="['color-box', { 'color-box-active': image === variant.image, 'color-box-sold-out': !variant.quantity }]"
                    :style="{backgroundColor: variant.color}"
                ></div>
            </div>

            <label for="sizes-list">Choose a size:</label>
            <select name="sizes-list" id="sizes-list">
                <option v-for="size in sizes" :key="size" :value="size">
                    {{ size }}
                </option>
            </select>

            <button
                v-on:click="addToCart"
                :disabled="!inStock"
                :class="[{ 'button-disabled': !inStock }]"
            >
                Add to Cart
            </button>
            <div class="cart">
                <p>Cart({{cart}})</p>
                <button v-on:click="removeFromCart">Remove element</button>
            </div>
        </div>

    </div>
</template>

<script>
  export default {
    name: 'Product',
    data: () => ({
      product: 'Socks',
      brand: 'Vue Mastery',
      selectedVariant: 0,
      details: ['80% cotton', '20% polyester', 'Unisex'],
      variants: [
        {
          id: '123',
          color: 'green',
          image: 'vmSocks-green-onWhite',
          quantity: 10,
          price: 3.99
        },
        {
          id: '321',
          color: 'darkblue',
          image: 'vmSocks-blue-onWhite',
          quantity: 0,
          price: 6.99
        },
        {
          id: '231',
          color: 'red',
          image: 'vmSocks-red-onWhite',
          quantity: 4,
          price: 4.99
        }
      ],
      sizes: ['xs', 's', 'm', 'l', 'xl'],
      cart: 0
    }),
    methods: {
      addToCart() {this.cart += 1},
      removeFromCart() {
        if (this.cart > 0) {
          this.cart -= 1
        }},
      changeSelectedProduct(index) {this.selectedVariant = index}
    },
    computed: {
      title() {
        return `${this.brand} ${this.product}`
      },
      image() {
        return this.variants[this.selectedVariant].image
      },
      inStock() {
        const selectedVariantObj = this.variants[this.selectedVariant]
        return !!selectedVariantObj.quantity
      }
    }
  }
</script>

<style scoped>
    body {
        font-family: tahoma;
        color:#282828;
        margin: 0px;
    }

    .product {
        display: flex;
        flex-flow: wrap;
        padding: 1rem;
    }

    img {
        border: 1px solid #d8d8d8;
        width: 70%;
        margin: 40px;
        box-shadow: 0 .5px 1px #d8d8d8;
    }

    .product-image {
        width: 80%;
    }

    .product-image,
    .product-info {
        margin-top: 10px;
        width: 50%;
    }

    .color-box {
        display: inline-block;
        width: 40px;
        height: 40px;
        margin-right: 5px;
    }
    .color-box-active {
        border: 2px solid #3fb1bb;
    }
    .color-box-sold-out {
        opacity: .3;
    }

    .cart {
        margin-right: 25px;
        float: right;
        border: 1px solid #d8d8d8;
        padding: 5px 20px;
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

    .review-form {
        width: 400px;
        padding: 20px;
        margin: 40px;
        border: 1px solid #d8d8d8;
    }

    input {
        width: 100%;
        height: 25px;
        margin-bottom: 20px;
    }

    textarea {
        width: 100%;
        height: 60px;
    }

    .tab {
        margin-left: 20px;
        cursor: pointer;
    }

    .activeTab {
        color: #16C0B0;
        text-decoration: underline;
    }
</style>
