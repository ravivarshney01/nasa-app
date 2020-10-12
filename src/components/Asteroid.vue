<template>
  <div class="bg-gray-100 rounded-lg hover:bg-gray-200 m-4 p-4">
    <div class="text-gray-900 font-bold text-xl mb-2">
      <a
        :href="asteroid.nasa_jpl_url"
        class="hover:text-gray-700"
        rel="noopener noreferrer"
        target="_blank"
      >
        {{ asteroid.name }} (ID - {{ asteroid.id }})
      </a>
    </div>
    <div class="">
      <p class="text-gray-600 mb-2">
        First observed on {{ asteroid.orbital_data.first_observation_date }}
      </p>
      <div class="flex-row">
        <p class="pr-2">
          Is it Hazardous?
          {{ asteroid.is_potentially_hazardous_asteroid }}; &nbsp;&nbsp; Is it
          Sentry Object? {{ asteroid.is_sentry_object }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Asteroid",
  props: ["asteroid"]
};
</script>

<style></style>
