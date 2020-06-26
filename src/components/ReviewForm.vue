<template>
    <div>
        <h3>Write a review</h3>
        <form class="review-form" v-on:submit.prevent="onSubmit">
            <p>
                <label for="name">Name:</label>
                <input :class="{'input-with-error': this.errors.indexOf('name') !== -1}" id="name" v-model="name">
                <span class="error-message" v-if="this.errors.indexOf('name') !== -1">Name is required</span>
            </p>

            <p>
                <label for="review">Review:</label>
                <textarea :class="{'input-with-error': this.errors.indexOf('review') !== -1}" id="review" v-model="review"></textarea>
                <span class="error-message" v-if="this.errors.indexOf('review') !== -1">Review is required</span>
            </p>

            <p>
                <label for="rating">Rating:</label>
                <select :class="{'input-with-error': this.errors.indexOf('rating') !== -1}" id="rating" v-model="rating">
                    <option>5</option>
                    <option>4</option>
                    <option>3</option>
                    <option>2</option>
                    <option>1</option>
                </select>
                <span class="error-message" v-if="this.errors.indexOf('review') !== -1">Rating is required</span>
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
      rating: null,
      errors: []
    }),
    methods: {
      onSubmit() {
        if (this.name && this.review && this.rating) {
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
            this.errors = []
        } else {
          if(!this.name) {
            this.errors.push('name')
          }
          if(!this.review) {
            this.errors.push('review')
          }
          if(!this.rating) {
            this.errors.push('rating')
          }
        }
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
.review-form label {
    font-weight: bold;
    font-size: 14px;
}
.review-form > p {
    position: relative;
    display: flex;
    flex-direction: column;
}
.error-message {
    font-size: 11px;
    color: darkred;
}
.input-with-error {
    border: solid 1px darkred;
}
</style>
