<template>
  <div>
    <h1>
      applicants for {{job.title}}
      <b-button to="/jobs">Back to jobs</b-button>
    </h1>
    <b-card class="mb-2">
      <template v-slot:header>
        <JobData :job="job" />
      </template>
      <h1>{{applicants.length}} Applicants</h1>
      <hr />
      <div v-for="(applicant, index) in applicants" :key="applicant.id">
        <b-row>
          <b-col md="4">
            <p>
              <small>applicant</small>
              {{index + 1}}
            </p>
            <small>name</small>
            <h2>{{applicant.name}}</h2>
            <small>email</small>
            <a :href="`mailto:${applicant.email}`">{{applicant.email}}</a>
          </b-col>
          <b-col md="8">
            <small>cover letter</small>
            <p>{{applicant.cover}}</p>
          </b-col>
        </b-row>
        <hr />
      </div>
    </b-card>
  </div>
</template>

<script>
import JobData from "@/components/JobData.vue";
export default {
  components: {
    JobData
  },
  middleware: "auth",
  data() {
    return {
      form: {}
    };
  },
  methods: {
    handleSubmit() {
      try {
        this.$axios.post(`/applicants`, {
          ...this.form,
          job: this.$route.params.id
        });
        this.$router.push("/success");
      } catch (err) {
        console.log(err);
      }
    }
  },
  async asyncData({ $axios, params }) {
    return {
      job: await $axios.$get(`/jobs/${params.id}`),
      applicants: await $axios.$get(`/applicants?job.id=${params.id}`)
    };
  }
};
</script>

<style scoped>
</style>