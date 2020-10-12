<template>
  <div :class="openTab === tabNo ? 'block' : 'hidden'">
    <slot name="content">
      Content of the tab
    </slot>
  </div>
</template>

<script>
export default {
  name: "TabContent",
  props: {
    openTab: Number,
    tabNo: Number
  }
};
</script>
