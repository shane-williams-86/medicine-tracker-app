<template>
  <div id="app">
    <!-- ====================================
  ——— HEADER
  ===================================== -->
    <header class="header" id="pageTop">
      <!-- Menu Zord -->
      <nav class="nav-menuzord navbar-sticky text-align-center">
        <div class="container clearfix">
          <h1 style="padding-top: 20px">Medicine Tracker</h1>
          <div id="menuzord" class="menuzord">
            <ul class="menuzord-menu menuzord-center">
              <li class="">
                <router-link class="" to="/">Home</router-link>
              </li>
              <li v-if="isLoggedIn()" class="">
                <router-link class="" to="/users/me">Profile</router-link>
              </li>
              <li v-if="isLoggedIn()" class="">
                <router-link class="" to="/patients">Patients</router-link>
              </li>
              <li v-if="!isLoggedIn()" class="">
                <router-link class="" to="/signup">Signup</router-link>
              </li>
              <li v-if="!isLoggedIn()" class="">
                <router-link class="" to="/login">Login</router-link>
              </li>
              <li v-if="isLoggedIn()" class="">
                <router-link class="" to="/logout">Logout</router-link>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </header>

    <router-view />
  </div>
</template>

<script>
export default {
  data: function () {
    return {};
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.jwt;
    },
  },
};
</script>
