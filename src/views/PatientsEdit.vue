<template>
  <div class="patients-edit">
    <h1>Edit Patient</h1>
    <form v-on:submit.prevent="updatePatient(patient)">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="patient.name" /><br />
      Notes:
      <input type="text" v-model="patient.notes" /><br />
      Image Url:
      <input type="text" v-model="patient.image_url" /><br />
      <input type="submit" value="Update" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      patient: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/patients/" + this.$route.params.id).then((response) => {
      console.log("patients show", response);
      this.photo = response.data;
    });
  },
  methods: {
    updatePatient: function (patient) {
      var editPatientParams = patient;
      axios
        .patch("/patients/" + patient.id, editPatientParams)
        .then((response) => {
          console.log("patients update", response);
          this.$router.push("/patients");
        })
        .catch((error) => {
          console.log("patients update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
