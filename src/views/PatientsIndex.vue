<template>
  <div class="patients-index">
    <h1>All Patients</h1>
    <div v-for="patient in patients" v-bind:key="patient.id">
      <h2>{{ patient.name }}</h2>
      <img v-bind:src="patient.image_url" v-bind:alt="patient.name" /><br />
      <button v-on:click="SeeDetails()">See Details</button>
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
    seeDetails: function () {},
  },
};
</script>
