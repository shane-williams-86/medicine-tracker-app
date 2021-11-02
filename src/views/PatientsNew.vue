<template>
  <div class="patients-new">
    <form v-on:submit.prevent="createPatient()">
      <h1>New Patient</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="newPatientParams.name" /><br />
      Notes:
      <input type="text" v-model="newPatientParams.notes" /><br />
      Image Url:
      <input type="text" v-model="newPatientParams.image_url" /><br />
      <input type="submit" value="Create" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newPatientParams: {},
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createPatient: function () {
      axios
        .post("/patients", this.newPatientParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/patients");
        })
        .catch((error) => {
          console.log("patients create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
