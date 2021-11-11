<template>
  <div class="signup">
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
                    Login
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
              type="email"
              class="form-control border-0 bg-smoke"
              required=""
              placeholder="Email"
              v-model="newSessionParams.email"
            />
          </div>

          <div class="form-group">
            <input
              type="password"
              class="form-control border-0 bg-smoke"
              placeholder="Password"
              v-model="newSessionParams.password"
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
<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newSessionParams: {},
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios.post("/sessions", this.newSessionParams).then((response) => {
        axios.defaults.headers.common["Authorization"] =
          "Bearer " + response.data.jwt;
        localStorage.setItem("jwt", response.data.jwt);
        this.$router.push("/users/me");
      });
    },
  },
};
</script>
