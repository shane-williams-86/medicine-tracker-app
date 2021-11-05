<template>
  <div class="patients-index">
    <div class="main-wrapper blog-list-fullwidth">
      <!-- ====================================
———	PAGE TITLE
===================================== -->
      <section class="page-title">
        <div
          class="page-title-img bg-img bg-overlay-darken"
          style="background-image: url(/assets/img/pages/page-title-bg4.jpg)"
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
                      Patients
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
——— TRAVEL LIST FULLWIDTH
===================================== -->
      <button v-on:click="addPatient(patient)">Add Patient</button> <br />
      <section class="py-9 py-md-10">
        <div class="container">
          <div
            v-for="patient in patients"
            v-bind:key="patient.id"
            class="card rounded-0 card-transparent border-bottom mb-7 pb-7"
          >
            <div class="row align-items-lg-center align-items-xl-stretch">
              <div class="col-md-6">
                <router-link
                  :to="`/patients/${patient.id}`"
                  class="position-relative"
                >
                  <img
                    v-bind:src="patient.image_url"
                    v-bind:alt="patient.name"
                    class="card-img-top rounded"
                  />
                  <div
                    class="card-img-overlay card-hover-overlay rounded"
                  ></div>
                </router-link>
              </div>

              <div class="col-md-6">
                <div class="card-body px-md-0 py-6 pt-md-0 pt-xl-6">
                  <h3 class="mb-4">
                    <a
                      href="blog-single-right-sidebar.html"
                      class="text-capitalize text-dark hover-text-primary"
                      >{{ patient.name }}</a
                    >
                  </h3>

                  <!-- <p class="mb-0">
                    Lorem ipsum dolor sit amet, consectetur adipisicing elit,
                    sed do eiusmod tempor incididunt ut labore et dolore magna
                    aliqua. Ut enim ad minim veniam, quis nostrud exercitation
                    ullamco.
                  </p> -->
                </div>

                <div class="card-footer px-5 px-lg-0">
                  <router-link
                    :to="`/patients/${patient.id}`"
                    class="btn btn-sm btn-outline-secondary text-uppercase"
                    >View Details</router-link
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
    <!-- element wrapper ends -->
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
