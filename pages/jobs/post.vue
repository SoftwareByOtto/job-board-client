<template>
  <div>
    <h1>Post job</h1>
    <b-card class="mb-2">
      <b-form @submit.prevent="handleSubmit">
        <b-form-group label="title">
          <b-form-input required v-model="form.title"></b-form-input>
        </b-form-group>
        <b-form-group label="description">
          <b-form-textarea rows="5" required v-model="form.description"></b-form-textarea>
        </b-form-group>

        <b-row>
          <b-col md="4">
            <b-form-group label="category">
              <b-form-input required v-model="form.category"></b-form-input>
            </b-form-group>
          </b-col>
          <b-col md="4">
            <b-form-group label="location">
              <b-form-input required v-model="form.location"></b-form-input>
            </b-form-group>
          </b-col>
          <b-col md="4">
            <b-form-group label="full time">
              <b-form-checkbox switch size="lg" required v-model="form.fulltime"></b-form-checkbox>
            </b-form-group>
          </b-col>
        </b-row>

        <b-button type="submit">submit</b-button>
      </b-form>
    </b-card>
  </div>
</template>

<script>
export default {
  middleware: "auth",
  data() {
    return {
      form: {}
    };
  },
  methods: {
    async handleSubmit() {
      try {
        const res = await this.$axios.post(`/jobs`, this.form);
        console.log("post", res);
        this.$router.push("/applicants");
      } catch (err) {
        console.log(err);
      }
    }
  }
};
</script>

<style scoped>
</style>