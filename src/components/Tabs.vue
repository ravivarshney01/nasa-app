<template>
  <ul class="flex mb-0 list-none flex-wrap pt-3 pb-4 flex-row" role="tablist">
    <tab-item
      :color="color"
      name="Asteroids"
      :openTab="openTab"
      :setOpenTab="setOpenTab"
      :tabNo="1"
    />
    <tab-item
      :color="color"
      name="Asteroids by Date"
      :openTab="openTab"
      :setOpenTab="setOpenTab"
      :tabNo="2"
    />
    <tab-item
      :color="color"
      name="Asteroid by ID"
      :openTab="openTab"
      :setOpenTab="setOpenTab"
      :tabNo="3"
    />
  </ul>
</template>
<script>
import TabItem from "./TabItem";

export default {
  name: "tabs",
  components: {
    TabItem
  },
  props: {
    setOpenTab: Function,
    color: String,
    openTab: Number
  }
};
</script>
