<template>
  <div>
    <h1>Login to an account</h1>
    <p>So you can post a job</p>
    <b-card class="mb-2">
      <b-form @submit.prevent="handleSubmit">
        <b-form-group label="company name or email">
          <b-form-input required v-model="form.identifier"></b-form-input>
        </b-form-group>
        <b-form-group label="password">
          <b-form-input type="password" required v-model="form.password"></b-form-input>
        </b-form-group>
        <b-button type="submit">submit</b-button>
      </b-form>
    </b-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        identifier: "fart@fart.com",
        password: "fart@fart.com"
      }
    };
  },
  methods: {
    async handleSubmit() {
      try {
        let response = await this.$auth.loginWith("local", { data: this.form });
        console.log(response);
        // this.$router.push("/success");
      } catch (err) {
        console.log(err);
      }
    }
  }
};
</script>

<style scoped>
</style>