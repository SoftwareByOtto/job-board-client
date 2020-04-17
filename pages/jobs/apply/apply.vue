<template>
  <div>
    <h1>
      Apply for {{job.title}}
      <b-button to="jobs">Back to jobs</b-button>
    </h1>
    <b-card class="mb-2">
      <template v-slot:header>
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
      <div class="d-flex justify-content-center">
        <b-button>apply now</b-button>
      </div>
      <hr />
      <h3>description</h3>
      {{job.description}}
    </b-card>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    return {
      job: await $axios.$get(`/jobs/${params.id}`)
    };
  }
};
</script>

<style scoped>
</style>