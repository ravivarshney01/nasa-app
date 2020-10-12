<template>
  <div>
    <label class="block text-gray-700 text-sm font-bold mb-2" for="id">
      ID of the Asteroid
    </label>
    <input
      id="id"
      class="shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
      type="text"
      v-model="id"
    />
    <button
      class="bg-teal-500 hover:bg-teal-700 text-white font-bold py-2 px-4 rounded mx-2"
      @click="search"
    >
      Search
    </button>

    <asteroid v-if="result" :asteroid="result" />
    <p v-if="err" class="text-red-500">{{ err }}</p>
  </div>
</template>

<script>
import axios from "axios";
import AsteroidVue from "./Asteroid.vue";
export default {
  name: "searchTab",
  components: {
    Asteroid: AsteroidVue
  },
  data: () => {
    return {
      id: null,
      result: null,
      err: null
    };
  },
  methods: {
    search() {
      axios
        .get(
          "https://api.nasa.gov/neo/rest/v1/neo/" +
            this.id +
            "/?api_key=Z7JVQif7Ntt7szEp8b0cQuZf8gFJ1Wo50FVh8San"
        )
        .then(res => {
          this.result = res.data;
          this.err = null;
        })
        .catch(() => {
          this.result = null;
          this.err =
            "No asteroid found with id " + this.id + ", please check id again";
        });
    }
  }
};
</script>

<style></style>
