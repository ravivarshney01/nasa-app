<template>
  <div class="">
    <p class="font-bold text-xl mb-5">Select maximum 7 day difference</p>
    <div class="flex flex-wrap -mx-3 mb-6">
      <div class="block px-3">
        <label
          class="block text-gray-700 text-sm font-bold mb-2"
          for="startDate"
        >
          Start Date
        </label>
        <input
          id="startDate"
          class="shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          type="date"
          v-model="startDate"
        />
      </div>
      <div class="block px-3">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="endDate">
          End Date
        </label>
        <input
          id="endDate"
          class="shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          type="date"
          v-model="endDate"
          :min="startDate"
        />
      </div>
      <div class="block px-3 self-end">
        <button
          class="bg-teal-500 hover:bg-teal-700 text-white font-bold py-2 px-4 rounded"
          @click="search"
        >
          Get
        </button>
      </div>
    </div>
    <div v-for="(asteroids, i) in asteroidsList" :key="i">
      <p class="text-lg font-semibold text-gray-500">
        Close Approach Date -
        {{ getDate(i) }}
      </p>
      <asteroid
        v-for="(asteroid, k) in asteroids.slice(0, limit)"
        :key="k"
        :asteroid="asteroid"
      />
      <p v-if="err" class="text-red-500">{{ err }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
import AsteroidVue from "./Asteroid.vue";
import { LIMIT } from "../constant";

export default {
  name: "dateSearch",
  data: () => {
    return {
      startDate: null,
      endDate: null,
      asteroidsList: [],
      limit: LIMIT,
      err: null
    };
  },
  methods: {
    search() {
      if (moment(this.startDate).add(7, "days") > moment(this.endDate)) {
        axios
          .get(
            "https://api.nasa.gov/neo/rest/v1/feed?start_date=" +
              this.startDate +
              "&end_date=" +
              this.endDate +
              "&detailed=true&api_key=Z7JVQif7Ntt7szEp8b0cQuZf8gFJ1Wo50FVh8San"
          )
          .then(res => {
            this.err = null;
            let i = 0;
            while (
              i <
              moment(this.endDate).diff(moment(this.startDate), "days") + 1
            ) {
              this.asteroidsList.push(
                res.data.near_earth_objects[
                  moment(this.startDate)
                    .add(i, "day")
                    .format("YYYY-MM-DD")
                ]
              );
              i++;
            }
          });
      } else {
        this.err = "Please check start and end dates, try again.";
        this.asteroidsList = [];
      }
    },
    getDate(i) {
      return moment(this.startDate)
        .add(i, "days")
        .format("YYYY-MM-DD");
    }
  },
  components: {
    Asteroid: AsteroidVue
  }
};
</script>

<style></style>
