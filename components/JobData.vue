<template>
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
</template>

<script>
export default {
  name: "JobData",
  props: { job: { type: Object, required: true } }
};
</script>

<style scoped>
</style>

