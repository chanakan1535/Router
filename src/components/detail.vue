<template>
  <v-container>
    <h1>Product Detail</h1>
    <h3>{{ productid }}</h3>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      productid: this.$route.params.id,
    };
  },
};
</script>

<style>
</style>