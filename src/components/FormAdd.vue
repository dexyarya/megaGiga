<template>
  <div class="container mt-5">
    <b-card
      header="Tambah Buku"
      header-tag="header"
      class="mb-2 p-3 mt-5"
      style="max-width: 80rem"
    >
      <form ref="form" v-on:submit.prevent="handleSubmit">
        <b-form-group
          label="Judul"
          label-for="title-input"
          invalid-feedback="TItle is required"
        >
          <b-form-input
            id="title-input"
            v-model="form.title"
            placeholder="Enter The Name"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          label="ISBN"
          label-for="isbn-input"
          invalid-feedback="ISBN is required"
          class="mt-3"
        >
          <b-form-input
            id="isbn-input"
            v-model="form.isbn"
            placeholder="Enter The ISBN"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          label="Pengarang"
          label-for="author-input"
          invalid-feedback="Author is required"
          class="mt-3"
        >
          <b-form-input
            id="author-input"
            v-model="form.author"
            placeholder="Enter The Author"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          label="Penerbit"
          label-for="publisher-input"
          invalid-feedback="Author is required"
          class="mt-3"
        >
          <b-form-input
            id="publisher-input"
            v-model="form.publisher"
            placeholder="Enter The Publisher"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          label="Description"
          label-for="description-input"
          invalid-feedback="Description is required"
          class="mt-3"
        >
          <b-form-textarea
            id="description-input"
            v-model="form.description"
            placeholder="Enter The Description"
            required
          ></b-form-textarea>
        </b-form-group>
      </form>

      <div class="button d-flex justify-content-between mb-5 mt-5">
        <router-link :to="{ name: 'dashboard' }">
          <b-button variant="danger">Kembali</b-button>
        </router-link>
        <b-button variant="primary" @click="handleSubmit">Simpan</b-button>
      </div>
    </b-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      form: {
        author: "",
        description: "",
        isbn: "",
        publisher: "",
        title: "",
      },
    };
  },

  methods: {
    async handleSubmit(e) {
      e.preventDefault();

      try {
        console.log("submited", this.form);
        const token = localStorage.getItem("token");

        const response = await axios.post(
          "http://159.223.57.121:8080/books",
          this.form,
          {
            headers: {
              Authorization: token,
            },
          }
        );
        if (response.status === 200) {
          this.$router.push("/dashboard");
        }
      } catch (error) {
        error.response;
        console.log(error.response);

        //   this.$swal({
        //     toast: true,
        //     position: "top-end",
        //     showConfirmButton: false,
        //     timer: 3000,
        //     icon: "error",
        //     text: "User has been not saved ",
        //   });
      }
    },
  },
};
</script>

<style></style>
