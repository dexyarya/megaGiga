<template>
  <div class="mt-5">
    <div class="container">
      <b-card header="Register" header-tag="header">
        <b-form ref="form" v-on:submit.prevent="onSubmit" v-if="show">
          <b-form-group
            id="input-group-1"
            label="User Name:"
            label-for="input-1"
            class="mt-2"
          >
            <b-form-input
              class="mt-2"
              id="input-1"
              v-model="form.username"
              placeholder="Enter User Name"
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
          <b-form-group
            class="mt-2"
            id="input-group-3"
            label="Profile Name:"
            label-for="input-3"
          >
            <b-form-input
              class="mt-2"
              id="input-3"
              v-model="form.profileName"
              placeholder="Enter Profile Name"
              required
            ></b-form-input>
          </b-form-group>
          <b-form-group
            class="mt-2"
            id="input-group-4"
            label="Address:"
            label-for="input-3"
          >
            <b-form-textarea
              class="mt-2"
              id="input-3"
              v-model="form.address"
              placeholder="Enter Address"
              required
            ></b-form-textarea>
          </b-form-group>

          <div class="d-flex mt-5">
            <b-button type="submit" @click="onSubmit" variant="primary"
              >Sign Up</b-button
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
        profileName: "",
        address: "",
      },
      show: true,
    };
  },
  methods: {
    async onSubmit(event) {
      event.preventDefault();
      try {
        const response = await axios.post(
          "http://159.223.57.121:8080/auth/do-register",
          this.form
        );
        alert("data berhasil di buat");
        console.log("ini register", response);
        await router.push("/");
      } catch (error) {
        console.log("ini register gagal", error);
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
