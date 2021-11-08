<template>
  <div class="patients-edit">
    <section class="py-9">
      <div class="container">
        <div class="hover-profile mb-7 mb-lg-9">
          <div class="row">
            <div class="col-md-6 col-lg-5 col-xl-4">
              <div class="mb-6 mb-md-0">
                <img
                  class="w-100"
                  :src="patient.image_url"
                  v-bind:alt="patient.name"
                />
              </div>
            </div>

            <div class="col-md-6 col-lg-7 col-xl-8">
              <div class="d-flex justify-content-between align-items-baseline">
                <div class="mb-6 mb-md-4 mb-lg-6">
                  <h2 class="text-uppercase font-weight-bold">
                    {{ patient.name }}
                  </h2>
                </div>

                <div class="icon-setting">
                  <a
                    href="javascript:void(0)"
                    data-bs-toggle="modal"
                    data-bs-target="#editPatient"
                  >
                    <i class="fas fa-pencil-alt" aria-hidden="true"></i>
                  </a>
                </div>
              </div>

              <ul class="list-unstyled">
                <li class="media media-profile-list">
                  <strong>Name:</strong>

                  <div class="media-body ms-2">
                    <span class="text-gray-color">{{ patient.name }}</span>
                  </div>
                </li>
                <li class="media media-profile-list">
                  <strong>Image URL:</strong>

                  <div class="media-body ms-2">
                    <span class="text-gray-color">{{ patient.image_url }}</span>
                  </div>
                </li>
                <li class="media media-profile-list">
                  <strong>Notes:</strong>

                  <div class="media-body ms-2">
                    <span class="text-gray-color">{{ patient.notes }}</span>
                  </div>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>
    <div
      class="modal fade"
      id="editPatient"
      tabindex="-1"
      role="dialog"
      aria-label="editPatientModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-sm modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header rounded">
            <h3 class="modal-title text-uppercase font-weight-bold">
              Edit Patient
            </h3>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>

          <div class="modal-body">
            <form v-on:submit.prevent="updatePatient()">
              <ul>
                <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
              </ul>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Name"
                  v-model="patient.name"
                />
              </div>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Image URL"
                  v-model="patient.image_url"
                />
              </div>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Notes"
                  v-model="patient.notes"
                />
              </div>

              <div class="d-grid">
                <button type="submit" class="btn btn-primary text-uppercase">
                  Update
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>

    <h1>Edit Patient</h1>
    <form v-on:submit.prevent="updatePatient(patient)">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="patient.name" /><br />
      Image Url:
      <input type="text" v-model="patient.image_url" /><br />
      Notes:
      <input type="text" v-model="patient.notes" /><br />
      <input type="submit" value="Update" />
      <button v-on:click="destroyDrug()">Delete Patient</button>
    </form>
  </div>
</template>

<script>
/* global $ */
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
      this.patient = response.data;
    });
  },
  methods: {
    updatePatient: function (patient) {
      var editPatientParams = patient;
      axios
        .patch("/patients/" + patient.id, editPatientParams)
        .then((response) => {
          console.log("patients update", response);
          $("#editPatient").modal("hide");
          this.patient = {};
          this.$router.push(`/patients/${this.patient.id}`);
        })
        .catch((error) => {
          console.log("patients update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
    destroyPatient: function (patient) {
      axios.delete("/patients/" + patient.id).then((response) => {
        console.log("patient destroy", response);
        var index = this.patient.indexOf(patient);
        this.patients.splice(index, 1);
      });
    },
  },
};
</script>
