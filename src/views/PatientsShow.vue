<template>
  <div class="patients-show">
    <router-link :to="`/patients/${patient.id}/edit`">Edit Patient</router-link>
    <h2>{{ patient.name }}</h2>
    <img :src="patient.image_url" v-bind:alt="patient.name" />
    <p>Patient Notes: {{ patient.notes }}</p>
    <div v-for="drug in patient.drugs" v-bind:key="drug.id">
      <p>Drug Name: {{ drug.name }}</p>
      <p>Description: {{ drug.description }}</p>
      <p>Frequency: {{ drug.frequency }}</p>
      <p>Notes: {{ drug.notes }}</p>
      <img :src="drug.image_url" v-bind:alt="drug.name" />
      <button v-on:click="showDrug(drug)">Details</button>
    </div>
    <h1>New Drug</h1>
    <div>
      Name:
      <input type="text" v-model="newDrugParams.name" /><br />
      Description:
      <input type="text" v-model="newDrugParams.description" /><br />
      Frequency:
      <input type="text" v-model="newDrugParams.frequency" /><br />
      Notes:
      <input type="text" v-model="newDrugParams.notes" /><br />
      Image Url:
      <input type="text" v-model="newDrugParams.image_url" /><br />
    </div>
    <dialog id="drug-details">
      <form method="dialog">
        <h1>Drug Info</h1>
        <p>Name: {{ currentDrug.name }}</p>
        <p>Notes: {{ currentDrug.notes }}</p>
        <p>Description: {{ currentDrug.description }}</p>
        <p>Image Url: {{ currentDrug.image_url }}</p>
        <p>Frequency: {{ currentDrug.frequency }}</p>
        <p>
          Name:
          <input type="text" v-model="currentDrug.name" />
        </p>
        <p>
          Notes:
          <input type="text" v-model="currentDrug.notes" />
        </p>
        <p>
          Description:
          <input type="text" v-model="currentDrug.description" />
        </p>
        <p>
          ImageUrl:
          <input type="text" v-model="currentDrug.image_url" />
        </p>
        <p>
          Frequency:
          <input type="text" v-model="currentDrug.frequency" />
        </p>
        <button v-on:click="newDrug(currentDrug)">Add Drug</button>
        <button v-on:click="updateDrug(currentDrug)">Update</button>
        <button v-on:click="destroyDrug(currentDrug)">Destroy Drug</button>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      patient: {},
      currentDrug: {},
      newDrugParams: {},
    };
  },
  created: function () {
    axios.get("/patients/" + this.$route.params.id).then((response) => {
      console.log("patients show", response.data);
      this.patient = response.data;
    });
  },
  methods: {
    showDrug: function (drug) {
      this.currentDrug = drug;
      document.querySelector("#drug-details").showModal();
    },
    updateDrug: function (drug) {
      var editDrugParams = drug;
      axios
        .patch("/drugs/" + drug.id, editDrugParams)
        .then((response) => {
          console.log("drugs update", response);
          this.currentDrug = {};
        })
        .catch((error) => {
          console.log("drugs update error", error.response);
        });
    },
    destroyDrug: function (drug) {
      axios.delete("/drugs/" + drug.id).then((response) => {
        console.log("drugs destroy", response);
        var index = this.drug.indexOf(drug);
        this.drug.splice(index, 1);
      });
    },
    addDrug: function () {
      axios
        .post("/drugs", this.newDrugParams)
        .then((response) => {
          console.log("drugs create", response);
          this.drugs.push(response.data);
          this.newDrugParams = {};
        })
        .catch((error) => {
          console.log("drugs create error", error.response);
        });
    },
  },
};
</script>
