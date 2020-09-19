<template>
  <div class="home">
    <h1>Adopt a new best friend.</h1>
    <p>{{ animalsCount }} animals ready for a new home!</p>
    <button class="btn btn-primary mb-2" @click="togglePetForm()">
      Add New Pet
    </button>
    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
      <!-- Name Input -->
      <b-form-group
        id="exampleInputGroup2"
        label="Pet's Name:"
        label-for="exampleInput2"
      >
        <b-form-input
          id="exampleInput2"
          type="text"
          v-model="formData.name"
          required
          placeholder="Enter name"
        />
      </b-form-group>
      <!-- Species Select -->
      <b-form-group
        id="exampleInputGroup3"
        label="Species:"
        label-for="exampleInput3"
      >
        <b-form-select
          id="exampleInput3"
          :options="['cats', 'dogs']"
          required
          v-model="formData.species"
        />
      </b-form-group>
      <!-- Age Input -->
      <b-form-group
        id="exampleInputGroup2"
        label="Pet's Age:"
        label-for="exampleInput2"
      >
        <b-form-input
          id="exampleInput2"
          type="number"
          v-model="formData.age"
          required
          placeholder="Enter age"
        />
      </b-form-group>
      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
export default {
  name: "Home",
  data() {
    return {
      showPetForm: false,
      formData: {
        name: "",
        species: "",
        age: 0,
      },
    };
  },
  computed: {
    ...mapGetters(["animalsCount", "getAllCats"]),
  },
  methods: {
    ...mapActions(["addPet"]),
    togglePetForm() {
      this.showPetForm = !this.showPetForm;
    },
    handleSubmit() {
      const { species, age, name } = this.formData;
      const payload = {
        species,
        pet: {
          name,
          age,
        },
      };
      this.addPet(payload);
      //reset the form
      this.formData = {
        name: "",
        species: "",
        age: 0,
      };
    },
  },
  components: {},
};
</script>
