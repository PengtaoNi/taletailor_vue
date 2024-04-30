<template>
  <!-- <div class="home">
    <h1 class="title">Welcome to TaleTailor</h1>
  </div> -->
  <div class="px-3 py-5 text-center">
    <h1 class="display-5 fw-bold text-body-emphasis" style="font-family: mali-bold;">Welcome to TaleTailor!</h1>
    <div class="col-lg-6 mx-auto">
      <p class="lead py-2 mb-4" style="font-family: mali; font-size: 18px">Our AI-powered storybooks empower your children to become the architects of their own adventures, offering customizable characters and themes that invite creativity to flourish in every tale.</p>
      <div class="d-grid gap-2 d-sm-flex justify-content-sm-center">
        <template v-if="$store.state.isAuthenticated">
          <router-link to="/dashboard/onboarding" class="btn btn-outline-primary btn-lg px-4 gap-3" aria-current="page" href="#" style="font-family: klee-bold;">Start HERE</router-link>
        </template>
        <template v-else>
          <router-link to="/dashboard/sign-up" class="btn btn-outline-primary btn-lg px-4 gap-3" aria-current="page" href="#" style="font-family: klee-bold;">Start HERE</router-link>
        </template>
      </div>
    </div>
    <div class="px-3 py-5 image-container" style="display: flex; align-items: center; justify-content: center; width: 100%; height: auto;">
      <img src="~@/assets/cover.jpg" alt="coverImage" style="max-width: 100%; height: auto; display: block;">
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeView',
  components: {
  }
}
</script>
