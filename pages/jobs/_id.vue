<template>
  <div>
    <h1>
      <n-link to="/jobs">Jobs</n-link>
    </h1>
    <b-card class="mb-2">
      <template v-slot:header>
        <JobData :job="job" />
      </template>
      <div class="d-flex justify-content-center">
        <b-button :to="`/jobs/apply/${job.id}`">apply now</b-button>
      </div>
      <hr />
      <h3>description</h3>
      {{job.description}}
    </b-card>
  </div>
</template>

<script>
import JobData from "@/components/JobData.vue";
export default {
  components: {
    JobData
  },
  async asyncData({ $axios, params }) {
    return {
      job: await $axios.$get(`/jobs/${params.id}`)
    };
  }
};
</script>

<style scoped>
</style>