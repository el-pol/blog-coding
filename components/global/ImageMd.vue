<template>
  <nuxt-img :src="imgSrc()" :alt="alt" sizes="sm:100vw md:50vw lg:400px" />
</template>

<script>
export default {
  props: {
    src: {
      type: String,
      required: true,
    },
    alt: {
      type: String,
      required: true,
    },
  },
  methods: {
    imgSrc() {
      try {
        return `/${this.src}`;
      } catch (error) {
        return null;
      }
    },
  },
};
</script>
