<template>
  <v-card class="fill-height">
    <v-img :src="movie.img"/>
    <v-card-title>
      <h2 class="subtitle-1">{{movie.title}}</h2>
    </v-card-title>
    <v-card-text>
      <v-rating small v-model="editRating"></v-rating>
      {{`${movie.rating}/5`}}
    </v-card-text>
  </v-card>
</template>

<style>
</style>

<script>
export default {
  props: {
    movie: Object
  },
  data: () => ({
    editRating: 0
  }),
  created() {
    this.editRating = this.$props.movie.rating;
  },
  watch: {
    editRating: function() {
      this.$emit("change-rating", this.editRating);
    }
  }
};
</script>
