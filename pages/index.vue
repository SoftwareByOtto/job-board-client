<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">Jobsite</h1>
      <h2 class="subtitle">{{jobsCount}} jobs and counting...</h2>
      <div class="links">
        <n-link to="jobs" class="button--green">Jobs</n-link>
        <n-link to="register" class="button--green">Register</n-link>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";

export default {
  async asyncData({ $axios, env }) {
    return { jobsCount: await $axios.$get(`/jobs/count`) };
  },
  components: {
    Logo
  }
};
</script>

<style scoped>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
