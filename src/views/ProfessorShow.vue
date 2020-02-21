<template>
  <div class="container">
    <h1 class="my-4">
      <small>Professor Reviews</small>
    </h1>

    <!-- Project One -->
    <div class="row">
      <div class="col-md-1">
        <div style="text-align: center;">Difficulty</div>
        <h1 style="text-align: center; vertical-align: text-top;">
          {{ professors.difficulty }}
        </h1>
      </div>
      <div class="col-md-10">
        <h3>{{ professors.title }} {{ professors.name }}</h3>
        <p>
          Sample professor review text goes here
        </p>
        <br />
        <br />
        <br />
      </div>
    </div>
    <a class="btn btn-secondary" href="../">Back To All Reviews</a>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      professors: []
    };
  },
  created: function() {
    axios.get("/professors/" + this.$route.params.id).then(response => {
      this.professors = response.data;
      console.log("professor: ", this.professors);
    });
  },
  methods: {}
};
</script>
