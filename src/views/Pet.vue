<template>
  <div>
    <h1>{{ animal.name }} ({{ formatSpecies }})</h1>
    <p>Age: {{ animal.age }} years old</p>
    <p>Breed: {{ animal.breed }}</p>
  </div>
</template>

<script>
import { mapState } from "vuex";
export default {
  data() {
    return {
      animal: {},
    };
  },
  computed: {
    ...mapState(["cats", "dogs"]),
    formatSpecies: function() {
      let original = this.$route.params.species;
      //make species uppercase
      original = original.charAt(0).toUpperCase() + original.slice(1);
      //remove 's' character from the end
      original = original.slice(0, -1);
      return original;
    },
  },
  mounted() {
    const animal = this[this.$route.params.species][this.$route.params.id];
    this.animal = animal;
  },
};
</script>

<style></style>
