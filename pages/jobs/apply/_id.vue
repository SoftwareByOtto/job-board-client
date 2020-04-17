<template>
  <div>
    <h1>
      Apply for {{job.title}}
      <b-button to="/jobs">Back to jobs</b-button>
    </h1>
    <b-card class="mb-2">
      <template v-slot:header>
        <JobData :job="job" />
      </template>
      <hr />
      <h3>application</h3>
      <b-form @submit.prevent="handleSubmit">
        <b-form-group label="name">
          <b-form-input required v-model="form.name"></b-form-input>
        </b-form-group>
        <b-form-group label="cover letter">
          <b-form-textarea required rows="10" v-model="form.cover"></b-form-textarea>
        </b-form-group>
        <b-form-group label="email">
          <b-form-input required type="email" v-model="form.email"></b-form-input>
        </b-form-group>
        <b-button type="submit">submit</b-button>
      </b-form>
    </b-card>
  </div>
</template>

<script>
import JobData from "@/components/JobData.vue";
export default {
  components: {
    JobData
  },
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
      job: await $axios.$get(`/jobs/${params.id}`)
    };
  }
};
</script>

<style scoped>
</style>