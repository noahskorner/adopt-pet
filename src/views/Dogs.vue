<template>
  <PetTable :pets="dogs" species="Dogs" />
</template>

<script>
import { mapState } from "vuex";
import PetTable from "@/components/PetTable";

export default {
  name: "Dogs",
  components: {
    PetTable,
  },
  data() {
    return {};
  },
  computed: {
    ...mapState(["dogs"]),
  },
};
</script>

<style></style>
