<template>
  <div id="wrapper">
    <nav class="navbar navbar-expand-lg" style="background-color: hsl(231, 100%, 90%);">
      <div class="container-fluid">
        <router-link to="/" class="navbar-brand" href="#">TaleTailor</router-link>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <template v-if="$store.state.isAuthenticated">
            <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <router-link to="/dashboard" class="nav-link active" aria-current="page" href="#">Dashboard</router-link>
              </li>
              <li class="nav-item">
                <router-link to="/dashboard/onboarding" class="btn btn-primary me-2" aria-current="page" href="#">New Story</router-link>
              </li>
              <li class="nav-item">
                <router-link to="/dashboard/my-account" class="btn btn-outline-primary me-2" aria-current="page" href="#">My account</router-link>
              </li>
            </ul>
          </template>
          <template v-else>
            <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <router-link to="/sign-up" class="btn btn-primary me-2" aria-current="page" href="#">Sign up</router-link>
              </li>
              <li class="nav-item">
                <router-link to="/log-in" class="btn btn-outline-primary me-2" aria-current="page" href="#">Log in</router-link>
              </li>
            </ul>
          </template>
        </div>
      </div>
    </nav>

    <section class="section">
      <router-view/>
    </section>

    <!-- <footer class="footer">
      <p class="has-text-centered">Copyright (c) 2024</p>
    </footer> -->
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'App',
    beforeCreate() {
      this.$store.commit('initializeStore')

      const token = this.$store.state.token

      if (token) {
        axios.defaults.headers.common['Authorization'] = "Token " + token
      } else {
        axios.defaults.headers.common['Authorization'] = ""
      }
    }
  }
</script>

<style lang="scss">
@font-face {
  font-family: mali;
  src: url('~@/assets/fonts/Mali-Regular.ttf');
}

@font-face {
  font-family: mali-bold;
  src: url('~@/assets/fonts/Mali-SemiBold.ttf');
}

@font-face {
  font-family: klee;
  src: url('~@/assets/fonts/KleeOne-Regular.ttf');
}

@font-face {
  font-family: klee-bold;
  src: url('~@/assets/fonts/KleeOne-SemiBold.ttf');
}

.navbar {
  font-family: mali;
}

// #wrapper {
//   background-color: hsl(330, 100%, 95%); /* This is Khaki; change the color code as desired */
// }
</style>
