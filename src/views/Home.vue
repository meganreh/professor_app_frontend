<template>
  <div class="container">
    <h1 class="my-4">
      <small>Professor Reviews</small>
    </h1>

    <!-- Project One -->
    <div v-for="professor in professors" class="row">
      <div class="col-md-1">
        <div style="text-align: center;">Difficulty</div>
        <h1 style="text-align: center; vertical-align: text-top;">
          {{ professor.difficulty }}
        </h1>
      </div>
      <div class="col-md-10">
        <h3>{{ professor.title }} {{ professor.name }}</h3>
        <p>
          Sample professor review text goes here
        </p>
        <a class="btn btn-secondary" href="#">See All Reviews</a>
        <br />
        <br />
        <br />
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
      professors: []
    };
  },
  created: function() {
    axios.get("/professors").then(response => {
      this.professors = response.data;
    });
  },
  methods: {}
};
</script>
