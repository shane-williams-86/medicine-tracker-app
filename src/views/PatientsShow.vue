<template>
  <div class="patients-show">
    <div class="main-wrapper blog-grid-two-col">
      <!-- ====================================
———	PAGE TITLE
===================================== -->
      <section class="page-title">
        <div class="page-title-img bg-img bg-overlay-darken">
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

    <section class="py-65">
      <h1 class="text-uppercase font-weight-bold" style="text-align: center">
        Patient Drugs
      </h1>
      <div class="" style="text-align: center">
        <a
          href="javascript:void(0)"
          data-bs-toggle="modal"
          data-bs-target="#addDrug"
          ><button type="submit" class="btn btn-primary text-uppercase">
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
              <a
                href="single-package-right-sidebar.html"
                class="position-relative"
              >
                <img
                  class="card-img-top"
                  :src="drug.image_url"
                  v-bind:alt="drug.name"
                />
              </a>

              <div class="card-body px-4">
                <h5>
                  <a
                    href="single-package-right-sidebar.html"
                    class="card-title text-uppercase"
                    >{{ drug.name }}</a
                  >
                </h5>
                <p class="mb-5">
                  {{ drug.notes }}
                </p>
                <p class="mb-5">Take {{ drug.frequency }}</p>
                <div class="d-flex justify-content-between align-items-center">
                  <div>
                    <p class="text-primary">{{ drug.description }}</p>
                  </div>
                  <div>
                    <button
                      v-on:click="showDrug(drug)"
                      class="btn btn-xs btn-outline-secondary text-uppercase"
                    >
                      Edit
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

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
          Image Url:
          <input type="text" v-model="currentDrug.image_url" />
        </p>
        <p>
          Frequency:
          <input type="text" v-model="currentDrug.frequency" />
        </p>
        <button v-on:click="updateDrug(currentDrug)">Update</button>
        <button v-on:click="destroyDrug()">Destroy Drug</button>
        <button>Close</button>
      </form>
    </dialog>
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
                  placeholder="Description"
                  v-model="newDrugParams.description"
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
                  placeholder="Image Url"
                  v-model="newDrugParams.image_url"
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
      document.querySelector("#drug-details").showModal();
    },
    updateDrug: function (drug) {
      var editDrugParams = drug;
      axios
        .patch("/drugs/" + drug.id, editDrugParams)
        .then((response) => {
          console.log("drugs update", response);
        })
        .catch((error) => {
          console.log("drugs update error", error.response);
        });
    },
    destroyDrug: function () {
      axios.delete("/drugs/" + this.currentDrug.id).then((response) => {
        console.log("drugs destroy", response);
        var index = this.patient.drugs.indexOf(this.currentDrug);
        this.patient.drugs.splice(index, 1);
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
      axios.delete("/patients/" + this.patient.id).then((response) => {
        console.log("patient destroy", response);
        $("#editPatient").modal("hide");
        this.$router.push("/patients");
      });
    },
  },
};
</script>
