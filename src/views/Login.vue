<template>
  <div class="login">
    <div style="text-align: center">
      <form v-on:submit.prevent="submit()">
        <h1>Login</h1>
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        <div>
          <label>Email:</label>
          <input type="email" v-model="newSessionParams.email" />
        </div>
        <div>
          <label>Password:</label>
          <input type="password" v-model="newSessionParams.password" />
        </div>
        <input type="submit" value="Submit" />
      </form>

      <div id="package-slider" class="owl-carousel owl-theme package-slider">
        <div class="item">
          <img class="" src="/assets/img/caretaker.jpeg" alt="image" />
        </div>
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
