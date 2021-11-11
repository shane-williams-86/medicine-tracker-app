<template>
  <div class="patients-show">
    <div class="main-wrapper blog-grid-two-col">
      <!-- ====================================
———	PAGE TITLE
===================================== -->
      <section class="page-title">
        <div
          class="page-title-img bg-img bg-overlay-darken"
          style="
            background-image: url(https://images.unsplash.com/photo-1563110493-198208247614?ixid=MnwxMjA3fDB8MHxzZWFyY2h8NTN8fHJlbGF4ZWR8ZW58MHx8MHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=60);
          "
        >
          <div class="container">
            <div
              class="row align-items-center justify-content-center"
              style="height: 200px"
            >
              <div class="col-lg-6">
                <div class="page-title-content">
                  <div class="title-border">
                    <h2 class="text-uppercase text-white font-weight-bold">
                      Patient
                    </h2>
                  </div>
                  <p class="text-white mb-0"></p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ====================================
——— PATIENTS INFO
===================================== -->
      <section class="py-9 py-md-10">
        <div class="container hover-profile">
          <div class="row">
            <div class="col-md-6 col-lg-5 col-xl-4">
              <div class="card card-transparent mb-7">
                <a
                  href="javascript:void(0)"
                  data-bs-toggle="modal"
                  data-bs-target="#editPatient"
                >
                  <img
                    v-bind:src="patient.image_url"
                    v-bind:alt="patient.name"
                    class="card-img-top rounded"
                  />
                </a>
              </div>
            </div>
            <div class="col-md-6 col-lg-7 col-xl-2">
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
                    <i class="fas fa-pencil-alt"></i>
                  </a>
                </div>
              </div>

              <ul class="list-unstyled">
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
      </section>
    </div>
    <!-- element wrapper ends -->

    <!-- ====================================
——— DRUGS INFO
===================================== -->

    <section class="py-75">
      <h1 class="text-uppercase font-weight-bold" style="text-align: center">
        Patient Drugs
      </h1>
      <div class="" style="text-align: center">
        <a
          href="javascript:void(0)"
          data-bs-toggle="modal"
          data-bs-target="#addDrug"
          ><button type="submit" class="btn btn-primary text-uppercase mb-2">
            Add Drug
          </button></a
        >
      </div>
      <div class="container">
        <div class="row">
          <div
            v-for="drug in patient.drugs"
            v-bind:key="drug.id"
            class="col-md-6 col-lg-4 mb-5"
          >
            <div class="card card-hover">
              <img
                class="card-img-top"
                :src="drug.image_url"
                v-bind:alt="drug.name"
              />

              <div class="card-body px-4">
                <h5 class="font-weight-bold">{{ drug.name }}</h5>
                <p class="mb-5">
                  {{ drug.notes }}
                </p>
                <p class="mb-5">Take {{ drug.frequency }}</p>
                <div class="d-flex justify-content-between align-items-center">
                  <div>
                    <p>{{ drug.description }}</p>
                  </div>

                  <a
                    href="javascript:void(0)"
                    data-bs-toggle="modal"
                    data-bs-target="#editDrug"
                    v-on:click="currentDrug = drug"
                  >
                    <i class="fas fa-pencil-alt"></i>
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Edit Patient Modal -->
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
                  Update</button
                ><br />
              </div>
            </form>
            <button
              v-on:click="destroyPatient()"
              class="btn btn-danger text-uppercase text-white"
            >
              Destroy
            </button>
          </div>
        </div>
      </div>
    </div>
    <!-- Add Drug Modal -->

    <div
      class="modal fade"
      id="addDrug"
      tabindex="-1"
      role="dialog"
      aria-label="addDrugModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-sm modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header rounded">
            <h3 class="modal-title text-uppercase font-weight-bold">
              Add Medication
            </h3>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>

          <div class="modal-body">
            <form v-on:submit.prevent="addDrug()">
              <ul>
                <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
              </ul>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Name"
                  v-model="newDrugParams.name"
                />
              </div>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Notes"
                  v-model="newDrugParams.notes"
                />
              </div>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Frequency"
                  v-model="newDrugParams.frequency"
                />
              </div>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Description"
                  v-model="newDrugParams.description"
                />
              </div>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Image URL"
                  v-model="newDrugParams.image_url"
                />
              </div>
              <div class="d-grid">
                <button type="submit" class="btn btn-primary text-uppercase">
                  Add Drug
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
    <!-- Edit Drug Modal -->
    <div
      class="modal fade"
      id="editDrug"
      tabindex="-1"
      role="dialog"
      aria-label="editDrugModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-sm modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header rounded">
            <h3 class="modal-title text-uppercase font-weight-bold">
              Edit Drug
            </h3>
          </div>

          <div class="modal-body">
            <form v-on:submit.prevent="updateDrug(currentDrug)">
              <ul>
                <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
              </ul>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Name"
                  v-model="currentDrug.name"
                />
              </div>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Image URL"
                  v-model="currentDrug.notes"
                />
              </div>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Notes"
                  v-model="currentDrug.frequency"
                />
              </div>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Notes"
                  v-model="currentDrug.description"
                />
              </div>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Notes"
                  v-model="currentDrug.image_url"
                />
              </div>

              <div class="d-grid">
                <button
                  type="submit"
                  class="btn btn-primary text-uppercase text-white"
                >
                  Update</button
                ><br />
              </div>
            </form>
            <button
              v-on:click="destroyDrug()"
              class="btn btn-danger text-uppercase text-white"
            >
              Destroy
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/* global $ */
import axios from "axios";
export default {
  data: function () {
    return {
      patient: {},
      currentDrug: {},
      newDrugParams: {},
      errors: [],
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
      document.querySelector("#editDrug").showModal();
    },
    updateDrug: function (drug) {
      var editDrugParams = drug;
      axios
        .patch("/drugs/" + drug.id, editDrugParams)
        .then((response) => {
          console.log("drugs update", response);
          $("#editDrug").modal("hide");
        })
        .catch((error) => {
          console.log("drugs update error", error.response);
        });
    },
    destroyDrug: function () {
      if (confirm("Are you sure you want to delete this Drug?"))
        axios.delete("/drugs/" + this.currentDrug.id).then((response) => {
          console.log("drugs destroy", response);
          var index = this.patient.drugs.indexOf(this.currentDrug);
          this.patient.drugs.splice(index, 1);
          $("#editDrug").modal("hide");
        });
    },
    addDrug: function () {
      var params = {
        name: this.newDrugParams.name,
        description: this.newDrugParams.description,
        notes: this.newDrugParams.notes,
        frequency: this.newDrugParams.frequency,
        image_url: this.newDrugParams.image_url,
        patient_id: this.patient.id,
      };
      axios
        .post("/drugs", params)
        .then((response) => {
          console.log("drugs create", response);
          $("#addDrug").modal("hide");
          this.patient.drugs.push(response.data);
          this.newDrugParams = {};
        })
        .catch((error) => {
          console.log("drugs create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
    updatePatient: function () {
      axios
        .patch("/patients/" + this.patient.id, this.patient)
        .then((response) => {
          console.log("patients update", response);
          $("#editPatient").modal("hide");
        })
        .catch((error) => {
          console.log("patients update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
    destroyPatient: function () {
      if (confirm("Are you sure you want to delete this Patient?"))
        axios.delete("/patients/" + this.patient.id).then((response) => {
          console.log("patient destroy", response);
          $("#editPatient").modal("hide");
          this.$router.push("/patients");
        });
    },
  },
};
</script>
