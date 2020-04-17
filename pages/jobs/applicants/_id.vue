<template>
  <div>
    <h1>
      applicants for {{job.title}}
      <b-button to="/jobs">Back to jobs</b-button>
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
      <h1>{{applicants.length}} Applicants</h1>
      <hr />
      <div v-for="(applicant, index) in applicants" :key="applicant.id">
        <p>Applicant {{index + 1}}</p>
        <h2>{{applicant.name}}</h2>
        <p>{{applicant.cover}}</p>
        <a :href="`mailto:${applicant.email}`">{{applicant.email}}</a>
        <hr />
      </div>
    </b-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {}
    };
  },
  methods: {
    handleSubmit() {
      try {
        this.$axios.post(`${process.env.API_URL}/applicants`, {
          ...this.form,
          job: this.$route.params.id
        });
        this.$router.push("/success");
      } catch (err) {
        console.log(err);
      }
    }
  },
  async asyncData({ $axios, params, env }) {
    return {
      job: await $axios.$get(`/jobs/${params.id}`),
      applicants: await $axios.$get(`/applicants?job.id=${params.id}`)
    };
  }
};
</script>

<style scoped>
</style>