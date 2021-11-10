<template>
  <div class="users-show">
    <!-- ====================================
——— PROFILE SECTION
===================================== -->
    <section class="py-9">
      <div class="container">
        <div class="hover-profile mb-7 mb-lg-9">
          <div class="row">
            <div class="col-md-6 col-lg-5 col-xl-4">
              <div class="mb-6 mb-md-0">
                <img
                  class="w-100"
                  :src="user.image_url"
                  v-bind:alt="user.name"
                />
              </div>
            </div>

            <div class="col-md-6 col-lg-7 col-xl-2">
              <div class="d-flex justify-content-between align-items-baseline">
                <div class="mb-6 mb-md-4 mb-lg-6">
                  <h2 class="text-uppercase font-weight-bold">
                    {{ user.name }}
                  </h2>
                </div>

                <div class="icon-setting">
                  <a
                    href="javascript:void(0)"
                    data-bs-toggle="modal"
                    data-bs-target="#editProfile"
                  >
                    <i class="fas fa-pencil-alt" aria-hidden="true"></i>
                  </a>
                </div>
              </div>

              <ul class="list-unstyled">
                <li class="media media-profile-list">
                  <strong>Phone:</strong>

                  <div class="media-body ms-2">
                    <span class="text-gray-color">{{ user.phone_number }}</span>
                  </div>
                </li>
                <li class="media media-profile-list">
                  <strong>Email:</strong>

                  <div class="media-body ms-2">
                    <span class="text-gray-color">{{ user.email }}</span>
                  </div>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Edit Modal -->
    <div
      class="modal fade"
      id="editProfile"
      tabindex="-1"
      role="dialog"
      aria-label="editProfileModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-sm modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header rounded">
            <h3 class="modal-title text-uppercase font-weight-bold">
              Edit your Profile
            </h3>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>

          <div class="modal-body">
            <form v-on:submit.prevent="updateUser()">
              <ul>
                <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
              </ul>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Name"
                  v-model="user.name"
                />
              </div>
              <div class="mb-3">
                <input
                  type="email"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Email"
                  v-model="user.email"
                />
              </div>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Phone Number"
                  v-model="user.phone_number"
                />
              </div>
              <div class="mb-3">
                <input
                  type="text"
                  class="form-control bg-smoke"
                  required=""
                  placeholder="Image Url"
                  v-model="user.image_url"
                />
              </div>
              <div class="d-grid">
                <button type="submit" class="btn btn-primary text-uppercase">
                  Update
                </button>
              </div>
            </form>
            <div class="text-uppercase text-center py-3">Or</div>
            <div class="d-grid">
              <button
                v-on:click="destroyUser()"
                class="btn btn-danger text-uppercase text-white"
              >
                Destroy Account
              </button>
            </div>
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
        $("#editProfile").modal("hide");
      });
    },
    destroyUser: function () {
      if (confirm("Are you sure you want to delete your Account?"))
        axios.delete("/users/me").then((response) => {
          console.log(response.data);
          $("#editProfile").modal("hide");
          this.$router.push("/signup");
          // route user back to signup
        });
    },
  },
};
</script>
