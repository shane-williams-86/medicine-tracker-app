<template>
  <div id="app">
    <!-- ====================================
  ——— HEADER
  ===================================== -->
    <header class="header" id="pageTop">
      <!-- Menu Zord -->
      <nav class="nav-menuzord navbar-sticky">
        <div class="container clearfix">
          <div id="menuzord" class="menuzord">
            <ul class="menuzord-menu menuzord-right">
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
