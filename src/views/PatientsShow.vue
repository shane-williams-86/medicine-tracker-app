<template>
  <div class="patients-show">
    <h2>{{ patient.name }}</h2>
    <p>{{ patient.notes }}</p>
    <img :src="patient.image_url" v-bind:alt="patient.name" />
    <div v-for="drug in patient.drugs" v-bind:key="drug.id">
      <p>{{ drug.name }}</p>
      <p>Description: {{ drug.description }}</p>
      <p>Frequency: {{ drug.frequency }}</p>
      <p>Notes: {{ drug.notes }}</p>
      <img :src="drug.image_url" v-bind:alt="drug.name" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      patient: {},
    };
  },
  created: function () {
    axios.get("/patients/" + this.$route.params.id).then((response) => {
      console.log("patients show", response.data);
      this.patient = response.data;
    });
  },
  methods: {},
};
</script>
