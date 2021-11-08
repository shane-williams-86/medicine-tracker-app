<template>
  <div class="patients-new">
    <div class="container">
      <div class="bg-smoke p-2 p-md-6 pb-6 pb-md-8 mb-9 rounded">
        <div class="row">
          <div class="col-12">
            <div class="row">
              <div class="col-lg-12">
                <div class="mb-4">
                  <h3 class="text-uppercase mb-3">Create New Patient</h3>
                  <p class="text-primary mb-0">Please complete forms below:</p>
                </div>

                <form v-on:submit.prevent="createPatient()">
                  <ul>
                    <li v-for="error in errors" v-bind:key="error">
                      {{ error }}
                    </li>
                  </ul>
                  <div class="form-group mb-4">
                    <input
                      type="text"
                      class="form-control form-control-lg rounded border-0"
                      required=""
                      placeholder="Patient Name"
                      v-model="newPatientParams.name"
                    />
                  </div>

                  <div class="form-group mb-4">
                    <input
                      type="text"
                      class="form-control form-control-lg rounded border-0"
                      required=""
                      placeholder="Notes"
                      v-model="newPatientParams.notes"
                    />
                  </div>

                  <div class="form-group mb-4">
                    <input
                      type="image_url"
                      class="form-control form-control-lg rounded border-0"
                      required=""
                      placeholder="Image URL"
                      v-model="newPatientParams.image_url"
                    />
                  </div>

                  <div class="pt-2">
                    <button
                      type="submit"
                      class="
                        btn btn-primary
                        text-uppercase
                        font-size-15
                        px-6 px-md-7
                      "
                    >
                      Create Patient
                    </button>
                  </div>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
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
