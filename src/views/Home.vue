<template>
  <div class="home">
    <h1>Home</h1>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",
  created() {
    axios
      .get(
        "https://api.nasa.gov/neo/rest/v1/neo/browse?page=1&size=10&api_key=Z7JVQif7Ntt7szEp8b0cQuZf8gFJ1Wo50FVh8San"
      )
      .then(res => {
        console.log(res);
      });
  }
};
</script>
