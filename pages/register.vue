<template>
  <div>
    <h1>Register an account</h1>
    <p>So you can post a job</p>
    <b-card class="mb-2">
      <b-form @submit.prevent="handleSubmit">
        <b-form-group label="company name">
          <b-form-input required v-model="form.username"></b-form-input>
        </b-form-group>
        <b-form-group label="email">
          <b-form-input required type="email" v-model="form.email"></b-form-input>
        </b-form-group>
        <b-form-group label="password">
          <b-form-input type="password" required v-model="form.password"></b-form-input>
        </b-form-group>
        <b-button type="submit">submit</b-button>
      </b-form>
      <hr />Already registered?
      <n-link to="/login">Login.</n-link>
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
    async handleSubmit() {
      try {
        const user = await this.$axios.post(`/auth/local/register`, this.form);
        console.log("user", user);
        const response = await this.$auth.loginWith("local", {
          data: {
            identifier: this.form.email,
            password: this.form.password
          }
        });
        console.log("res", response);
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