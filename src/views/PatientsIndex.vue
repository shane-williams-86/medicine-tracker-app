<template>
  <div class="patients-index">
    <button v-on:click="addPatient(patient)">Add Patient</button> <br />
    <h1>All Patients</h1>
    <div v-for="patient in patients" v-bind:key="patient.id">
      <h2>{{ patient.name }}</h2>
      <img v-bind:src="patient.image_url" v-bind:alt="patient.name" /><br />
      <router-link :to="`/patients/${patient.id}`">More Info</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      patients: [],
      currentPatient: {},
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
    addPatient: function (patient) {
      this.patients = patient;
      console.log("patients-show");
      this.$router.push("/patients/new");
    },
  },
};
</script>
