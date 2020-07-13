<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
    <div>
        <div class="product">
            <div class="product-images">
                <img v-for="(image, index) in images" :key="image" v-on:mouseover="changeImage(index)" :src="require(`../assets/${image}.jpg`)" />
            </div>
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

        <Tabs>
            <Tab id="list-reviews" title="Reviews">
                <div>
                    <h2>Reviews</h2>
                    <p>{{ current }}</p>
                    <p v-if="!reviews.length">There are no reviews for this product yet.</p>
                    <ul v-else>
                        <li v-for="review in reviews" :key="review.name">
                            <p>{{ review.name }}</p>
                            <p>{{ review.rating }}</p>
                            <p>{{ review.review }}</p>
                        </li>
                    </ul>
                </div>
            </Tab>

            <Tab id="add-review" title="Write a review">
                <ReviewForm v-on:review-submit="handleFormSubmit" />
            </Tab>
        </Tabs>
    </div>
</template>

<script>
  import ReviewForm from './ReviewForm'
  import Tabs from './Tabs'
  import Tab from './Tab'

  export default {
    name: 'Product',
    components: {ReviewForm, Tabs, Tab},
    data: () => ({
      selectedVariant: 0,
      selectedImage: 0,
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
      changeSelectedProduct(index) {
        this.selectedVariant = index
        this.selectedImage = 0
      },
      handleFormSubmit(reviewObj) {
        this.reviews.push(reviewObj)
      },
      changeImage (index) {
        this.selectedImage = index
      }
    },
    computed: {
      title() {
        const selectedVariantObj = this.product.variants[this.selectedVariant]
        return `${selectedVariantObj.brand} ${selectedVariantObj.name}`
      },
      image() {
        const list = this.product.variants[this.selectedVariant].images
        return list[this.selectedImage]
      },
      images() {
        return this.product.variants[this.selectedVariant].images
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
        padding: 1rem;
    }

    img {
        border: 1px solid #d8d8d8;
        box-shadow: 0 .5px 1px #d8d8d8;
    }

    .product-images {
        display: flex;
        flex-direction: column;
    }

    .product-images img {
        width: 50px;
    }

    .product-images img:not(:first-child) {
        margin-top: 8px;
    }

    .product-image {
        padding: 0 40px;;
        width: 30%;
    }

    .product-image img {
        width: 100%;
    }

    .product-info {
        flex-grow: 1;
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

</style>
