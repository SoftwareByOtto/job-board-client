<template>
  <div>
    <h1>Jobs</h1>
    <b-form-group description="choose a category">
      <b-form-select v-model="filterCategory" :options="options"></b-form-select>
    </b-form-group>
    <div v-for="job in filteredJobs" :key="job.id">
      <n-link :to="`/jobs/${job.id}`">
        <b-card class="mb-2" :class="{promoted: job.owner && job.owner.promoted}">
          <b-row>
            <b-col md="6">
              <p v-if="job.owner">{{job.owner.username}}</p>
              <h2>{{job.title}}</h2>
              <p>{{job.fulltime ? 'Full-time' : 'Part-time'}} / {{job.location}}</p>
              <b-badge v-if="job.category">{{job.category}}</b-badge>
            </b-col>
            <b-col md="6" class="d-flex justify-content-center align-items-center">
              <h4>{{job.created_at}}</h4>
            </b-col>
          </b-row>
        </b-card>
      </n-link>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, env }) {
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