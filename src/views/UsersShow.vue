<template>
  <div class="users-show">
    <h2>{{ user.name }}</h2>
    <p>{{ user.phone_number }}</p>
    <img :src="user.image_url" v-bind:alt="user.name" />
    <form v-on:submit.prevent="updateUser()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="user.name" />
      </div>
      <div>
        <label>Email:</label>
        <input type="email" v-model="user.email" />
      </div>
      <div>
        <label>Phone Number:</label>
        <input type="text" v-model="user.phone_number" />
      </div>
      <div>
        <label>Image Url:</label>
        <input type="text" v-model="user.image_url" />
      </div>
      <input type="submit" value="Submit" />
    </form>
    <button v-on:click="destroyUser()">Destroy Account</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      user: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/users/me").then((response) => {
      console.log("users show", response.data);
      this.user = response.data;
    });
  },
  methods: {
    updateUser: function () {
      axios.patch("/users/me", this.user).then((response) => {
        console.log(response.data);
      });
    },
    destroyUser: function () {
      axios.delete("/users/me").then((response) => {
        console.log(response.data);
        this.$router.push("/signup");
        // route user back to signup
      });
    },
  },
};
</script>
