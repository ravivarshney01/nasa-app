<template>
  <li class="mb-2 mr-2 last:mr-0 flex-auto text-center cursor-pointer">
    <a
      class="text-xs font-bold uppercase px-5 py-3 shadow-md rounded block leading-normal"
      :class="
        openTab === tabNo
          ? 'text-white bg-' + color + '-500'
          : 'text-' + color + '-500 bg-white'
      "
      @click="setOpenTab(tabNo)"
      data-toggle="tab"
      role="tablist"
    >
      {{ name }}
    </a>
  </li>
</template>
<script>
export default {
  name: "tabitem",
  props: {
    name: String,
    setOpenTab: Function,
    color: String,
    openTab: Number,
    tabNo: Number
  }
};
</script>
