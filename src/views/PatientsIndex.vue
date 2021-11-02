<template>
  <div class="patients-index">
    <button>Add Patient</button> <br />
    <h1>All Patients</h1>
    <div v-for="patient in patients" v-bind:key="patient.id">
      <h2>Patient: {{ patient.name }}</h2>
      <img v-bind:src="patient.image_url" v-bind:alt="patient.name" /><br />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      patients: [],
    };
  },
  created: function () {
    this.indexPatients();
  },
  methods: {
    indexPatients: function () {
      axios.get("/patients").then((response) => {
        console.log("patients index", response);
        this.patients = response.data;
      });
    },
  },
};
</script>
