<template>
  <div>
    <h1>Your Jobs</h1>
    <p>jobs you've posted</p>
    <b-form-group description="choose a category">
      <b-form-select v-model="filterCategory" :options="options"></b-form-select>
    </b-form-group>
    <div v-for="job in filteredJobs" :key="job.id">
      <n-link :to="`/applicants/${job.id}`">
        <b-card class="mb-2" :class="{ promoted: job.owner && job.owner.promoted }">
          <JobData :job="job" />
        </b-card>
      </n-link>
    </div>
  </div>
</template>

<script>
import JobData from "@/components/JobData.vue";
export default {
  components: {
    JobData
  },
  middleware: "auth",
  async asyncData({ $axios, $auth }) {
    return { jobs: await $axios.$get(`/jobs?owner=${$auth.user.id}`) };
  },
  data() {
    return {
      filterCategory: ""
    };
  },
  computed: {
    options() {
      return [
        { value: null, text: "choose an option" },
        ...[...new Set(this.jobs.map(job => job.category))].map(v => ({
          value: v,
          text: v
        }))
      ];
    },
    filteredJobs() {
      return this.filterCategory
        ? this.jobs.filter(job => job.category === this.filterCategory)
        : this.jobs;
    }
  }
};
</script>

<style scoped>
.promoted {
  border-right: 10px solid gold;
}
</style>
