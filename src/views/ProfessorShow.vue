<template>
  <div class="container">
    <h1 class="my-4">
      <small>Professor Reviews</small>
    </h1>

    <!-- Project One -->
    <div class="row">
      <div class="col-md-2">
        <div style="text-align: center;">Difficulty</div>
        <h1 style="text-align: center; vertical-align: text-top;">
          {{ professor.difficulty }}
        </h1>
      </div>
      <div class="col-md-10">
        <h3>{{ professor.title }} {{ professor.name }}</h3>
        <div v-for="review in professor.reviews">
          <p>
            Rating: {{ review.rating }}
            <br />
            {{ review.text }}
          </p>
        </div>
      </div>
    </div>
    <a class="btn btn-secondary" href="../">Back To All Reviews</a>

    <br />
    <br />

    <div id="addReview">
      <div class="container">
        <h3>Leave a Review</h3>
        <form v-on:submit.prevent="createReview()">
          Rating:
          <input type="number" v-model="newReviewRating" min="1" max="5" />
          <br />
          Review:
          <input type="text" v-model="newReviewText" />
          <br />
          <br />
          <input class="btn btn-dark" type="submit" value="Submit" />
        </form>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      reviews: [],

      professor: {},
      newReviewRating: "",
      newReviewText: "",
      errors: []
    };
  },
  created: function() {
    axios.get("/professors/" + this.$route.params.id).then(response => {
      this.professor = response.data;
      console.log("professor: ", this.professor);
    });
  },
  methods: {
    createReview: function() {
      var params = {
        professor_id: this.professor.id,
        text: this.newReviewText,
        rating: this.newReviewRating
      };
      axios
        .post("/reviews", params)
        .then(response => {
          this.$router.push("/");
        })
        .catch(error => {
          console.log(error.response);
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>
