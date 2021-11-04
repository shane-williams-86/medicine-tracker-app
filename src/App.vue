<template>
  <div id="app">
    <!-- ====================================
  ——— HEADER
  ===================================== -->
    <header class="header" id="pageTop">
      <!-- Menu Zord -->
      <nav class="nav-menuzord nav-menuzord-transparent navbar-sticky">
        <div class="container clearfix">
          <div id="menuzord" class="menuzord">
            <a href="index.html" class="menuzord-logo-brand"></a>

            <ul class="menuzord-menu menuzord-right">
              <li>
                <router-link to="/users/me">Profile</router-link>
              </li>
              <li>
                <router-link to="/patients">Patients</router-link>
              </li>
              <li v-if="!isLoggedIn()">
                <router-link to="/signup">Signup</router-link>
              </li>
              <li v-if="isLoggedIn()">
                <router-link to="/logout">Logout</router-link>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </header>
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/users/me">Profile</router-link> |
      <router-link v-if="!isLoggedIn()" to="/signup">Signup</router-link> |
      <router-link v-if="!isLoggedIn()" to="/login">Login</router-link> |
      <router-link v-if="isLoggedIn()" to="/logout">Logout</router-link> |
      <router-link to="/patients">Patients</router-link> |
      <router-link to="/patients/new">New Patient</router-link> |
    </div> -->

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
