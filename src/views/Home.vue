<template>
  <div class="container mx-auto">
    <tabs :openTab="openTab" :setOpenTab="setOpenTab" :color="color" />
    <div
      class="relative flex flex-col min-w-0 break-words bg-white w-full mb-6 "
    >
      <div class="px-4 py-5 flex-auto">
        <div class="tab-content tab-space">
          <tab-content :openTab="openTab" :tabNo="1">
            <template slot="content">
              <Asteroid
                v-for="(asteroid, i) in asteroids"
                :key="i"
                :asteroid="asteroid"
              />
              <button
                class="bg-teal-500 hover:bg-teal-700 text-white font-bold py-2 px-4 rounded mx-2"
                @click="loadMore"
              >
                Load More
              </button>
            </template>
          </tab-content>
          <tab-content :openTab="openTab" :tabNo="2">
            <template slot="content">
              <date-search />
            </template>
          </tab-content>
          <tab-content :openTab="openTab" :tabNo="3">
            <template slot="content">
              <search-tab />
            </template>
          </tab-content>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import AsteroidVue from "../components/Asteroid.vue";
import TabsVue from "../components/Tabs.vue";
import TabContentVue from "../components/TabContent.vue";
import SearchTabVue from "../components/SearchTab.vue";
import DateSearchVue from "../components/DateSearchTab.vue";
import { LIMIT } from "../constant";

export default {
  name: "Home",
  components: {
    Asteroid: AsteroidVue,
    Tabs: TabsVue,
    TabContent: TabContentVue,
    SearchTab: SearchTabVue,
    DateSearch: DateSearchVue
  },
  data: () => {
    return {
      openTab: 1,
      color: "teal",
      asteroids: [],
      page: 1
    };
  },
  methods: {
    setOpenTab(k) {
      this.openTab = k;
    },
    loadMore() {
      this.page++;
      axios
        .get(
          "https://api.nasa.gov/neo/rest/v1/neo/browse?page=" +
            this.page +
            "&size=" +
            LIMIT +
            "&api_key=Z7JVQif7Ntt7szEp8b0cQuZf8gFJ1Wo50FVh8San"
        )
        .then(res => {
          this.asteroids.push(...res.data.near_earth_objects);
        });
    }
  },
  created() {
    axios
      .get(
        "https://api.nasa.gov/neo/rest/v1/neo/browse?page=1&size=" +
          LIMIT +
          "&api_key=Z7JVQif7Ntt7szEp8b0cQuZf8gFJ1Wo50FVh8San"
      )
      .then(res => {
        this.asteroids = res.data.near_earth_objects;
      });
  }
};
</script>
