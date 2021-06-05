<template>
  <header class="mb-4 flex justify-between items-center">
    <NuxtLink to="/"><Logo :svg-color="svgColor" /></NuxtLink>
    <AppSearchInput class="ml-8" />
  </header>
</template>
<script>
export default {
  props: {
    svgColor: {
      type: String,
      default: "white",
    },
  },
};
</script>
