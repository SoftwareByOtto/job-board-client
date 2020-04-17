<template>
  <div>
    <h1>Jobs</h1>
    <b-form-group description="choose a category">
      <b-form-select v-model="filterCategory" :options="options"></b-form-select>
    </b-form-group>
    <div v-for="job in filteredJobs" :key="job.id">
      <n-link :to="`/jobs/${job.id}`">
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
  async asyncData({ $axios }) {
    return { jobs: await $axios.$get(`/jobs`) };
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
