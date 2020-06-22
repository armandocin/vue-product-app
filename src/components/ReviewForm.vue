<template>
    <div>
        <h3>Write a review</h3>
        <form class="review-form" v-on:submit.prevent="onSubmit">
            <p>
                <label for="name">Name:</label>
                <input id="name" v-model="name">
            </p>

            <p>
                <label for="review">Review:</label>
                <textarea id="review" v-model="review"></textarea>
            </p>

            <p>
                <label for="rating">Rating:</label>
                <select id="rating" v-model="rating">
                    <option>5</option>
                    <option>4</option>
                    <option>3</option>
                    <option>2</option>
                    <option>1</option>
                </select>
            </p>
            <p>
                <input type="submit" value="Submit">
            </p>
        </form>
    </div>
</template>

<script>
  export default {
    name: 'ReviewForm',
    data: () => ({
      name: null,
      review: null,
      rating: null
    }),
    methods: {
      onSubmit() {
        this.$emit(
          'review-submit',
          {
            name: this.name,
            review: this.review,
            rating: this.rating
          }
        )

        this.name = null
        this.review = null
        this.rating = null
      }
    }
  }
</script>

<style scoped>
.review-form {
    width: 400px;
    padding: 20px;
    margin: 40px;
    border: 1px solid #d8d8d8;
}
</style>
