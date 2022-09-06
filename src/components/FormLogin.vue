<template>
  <div class="mt-5">
    <div class="container">
      <b-card header="Login" header-tag="header">
        <b-form ref="form" v-on:submit.prevent="onSubmit" v-if="show">
          <b-form-group
            id="input-group-1"
            label="Username:"
            label-for="input-1"
            class="mt-2"
          >
            <b-form-input
              class="mt-2"
              id="input-1"
              v-model="form.username"
              placeholder="Enter Username"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group
            class="mt-2"
            id="input-group-2"
            label="Password:"
            label-for="input-2"
          >
            <b-form-input
              class="mt-2"
              id="input-2"
              type="password"
              v-model="form.password"
              placeholder="Enter Password"
              required
            ></b-form-input>
          </b-form-group>

          <div class="d-flex mt-3 mb-3">
            <b-button type="submit" @click="onSubmit" variant="primary"
              >Login</b-button
            >
          </div>

          <a href="#" class="mt-5">forget passsword?</a>

          <div class="d-flex mt-3 mb-3">
            <b-button type="submit" :to="{ name: 'register' }" variant="primary"
              >Register</b-button
            >
          </div>
        </b-form>
      </b-card>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      form: {
        username: "",
        password: "",
      },
      show: true,
    };
  },
  methods: {
    async onSubmit(event) {
      event.preventDefault();
      try {
        const response = await axios.post(
          "http://159.223.57.121:8080/auth/do-login",
          this.form
        );
        console.log("ini register", response);

        if (response.data.message === "LOGIN SUCCESS") {
          this.$router.push("/dashboard");
        } else {
          alert("password / username salah");
        }

        localStorage.setItem("token", response.data.data.token);
      } catch (error) {
        console.log("ini register gagal", error);
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
