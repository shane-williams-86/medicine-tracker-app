<template>
  <div class="signup">
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
                    Signup
                  </h2>
                </div>
                <p class="text-white mb-0"></p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <div class="row">
      <div class="col-xl-4"></div>
      <div class="col-md-6 col-lg-7 col-xl-4 mb-6">
        <form v-on:submit.prevent="submit()">
          <ul>
            <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
          </ul>
          <div class="form-group">
            <input
              type="text"
              class="form-control border-0 bg-smoke"
              required=""
              placeholder="Your Name"
              v-model="newUserParams.name"
            />
          </div>

          <div class="form-group">
            <input
              type="email"
              class="form-control border-0 bg-smoke"
              placeholder="Your Email"
              v-model="newUserParams.email"
            />
          </div>

          <div class="form-group">
            <input
              type="password"
              class="form-control border-0 bg-smoke"
              placeholder="Password"
              v-model="newUserParams.password"
            />
          </div>
          <div class="form-group">
            <input
              type="password"
              class="form-control border-0 bg-smoke"
              placeholder="Password"
              v-model="newUserParams.password_confirmation"
            />
          </div>

          <div class="d-flex justify-content-end">
            <button type="submit" class="btn btn-primary text-uppercase">
              Submit
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newUserParams: {},
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/users", this.newUserParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/login");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
