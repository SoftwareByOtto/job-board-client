<template>
  <div>
    <h1>Jobs</h1>
    <div v-for="job in jobs" :key="job.id">
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
  }
};
</script>

<style scoped>
.promoted {
  border-right: 10px solid gold;
}
</style>