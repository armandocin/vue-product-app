<template>
    <div>
        <div class="product">
            <div class="product-image">
                <img v-bind:src="require(`../assets/${image}.jpg`)" />
            </div>

            <div class="product-info">
                <h1>{{ title }}</h1>
                <!-- v-show is more performant than if-else-->
                <p v-show="product.variants[selectedVariant].quantity >= 10">In Stock</p>
                <p v-show="product.variants[selectedVariant].quantity < 10 && product.variants[selectedVariant].quantity > 0">Almost sold out!</p>
                <p v-show="!product.variants[selectedVariant].quantity">Out of Stock</p>

                <ul>
                    <li :key="detail" v-for="detail in product.variants[selectedVariant].details">{{ detail }}</li>
                </ul>

                <div>
                    <div
                        :key="variant.id"
                        v-for="(variant, index) in product.variants"
                        v-on:mouseover="changeSelectedProduct(index)"
                        :class="['color-box', { 'color-box-active': selectedVariant === index, 'color-box-sold-out': !variant.quantity }]"
                        :style="{backgroundColor: variant.color}"
                    ></div>
                </div>

                <label for="sizes-list">Choose a size:</label>
                <select name="sizes-list" id="sizes-list">
                    <option v-for="size in product.variants[selectedVariant].sizes" :key="size" :value="size">
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
            </div>
        </div>

        <div>
            <h2>Reviews</h2>
            <p v-if="!reviews.length">There are no reviews for this product yet.</p>
            <ul v-else>
                <li v-for="review in reviews" :key="review.name">
                    <p>{{ review.name }}</p>
                    <p>{{ review.rating }}</p>
                    <p>{{ review.review }}</p>
                </li>
            </ul>
        </div>

        <ReviewForm v-on:review-submit="handleFormSubmit" />
    </div>
</template>

<script>
  import ReviewForm from './ReviewForm'

  export default {
    name: 'Product',
    components: {ReviewForm},
    data: () => ({
      selectedVariant: 0,
      reviews: []
    }),
    props: {
      product: {Object}
    },
    methods: {
      addToCart() {
        this.$emit(
          'add-to-cart',
          this.product.variants[this.selectedVariant]
        )
      },
      changeSelectedProduct(index) {this.selectedVariant = index},
      handleFormSubmit(reviewObj) {
        this.reviews.push(reviewObj)
      }
    },
    computed: {
      title() {
        const selectedVariantObj = this.product.variants[this.selectedVariant]
        return `${selectedVariantObj.brand} ${selectedVariantObj.name}`
      },
      image() {
        return this.product.variants[this.selectedVariant].image
      },
      inStock() {
        const selectedVariantObj = this.product.variants[this.selectedVariant]
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
