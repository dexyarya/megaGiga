<template>
  <div class="container">
    <b-card
      header="Update Buku"
      header-tag="header"
      class="mb-2 p-3 mt-5"
      style="max-width: 80rem"
    >
      <b-form @submit="onUpdate" v-if="show">
        <b-form-group id="input-group-2" label="Judul:" label-for="input-2">
          <b-form-input
            id="input-2"
            v-model="form.title"
            placeholder="Masukan Judul Buku"
            required
            class="mb-3"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-1" label="ISBN:" label-for="input-1">
          <b-form-input
            id="input-1"
            v-model="form.isbn"
            placeholder="Masukan ISBN"
            required
            class="mb-3"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-3" label="Penerbit:" label-for="input-3">
          <b-form-input
            id="input-3"
            v-model="form.publisher"
            placeholder="Masukan Nama Penerbit"
            required
            class="mb-3"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-4" label="Pembuat:" label-for="input-4">
          <b-form-input
            id="input-4"
            v-model="form.author"
            placeholder="Masukan Nama Pembuat"
            required
            class="mb-3"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-5" label="Deskripsi:" label-for="input-5">
          <b-form-textarea
            id="input-5"
            v-model="form.description"
            placeholder="Enter Deskripsi"
            required
            class="mb-3"
          ></b-form-textarea>
        </b-form-group>

        <!-- <div class="text-center">
        <b-button type="submit" variant="danger" class="mx-3">Update</b-button>
        <router-link to="/dashboard" class="navbar-brand">
          <b-button variant="primary" class="mx-3">Kembali</b-button>
        </router-link>
      </div> -->

        <div class="button d-flex justify-content-between mb-5 mt-5">
          <router-link :to="{ name: 'dashboard' }">
            <b-button variant="danger">Kembali</b-button>
          </router-link>
          <b-button variant="primary" type="submit">Update</b-button>
        </div>
      </b-form>
    </b-card>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      result: {},
      form: {
        author: "",
        description: "",
        isbn: "",
        publisher: "",
        title: "",
        id: 0,
      },
      show: true,
    };
  },
  mounted() {
    this.onLoad();
  },
  methods: {
    async onLoad() {
      const id = this.$route.params.id;
      const token = localStorage.getItem("token");
      const data = await axios.get(
        `http://159.223.57.121:8080/books/findbyid/${id}`,
        {
          headers: {
            Authorization: token,
          },
        }
      );
      console.log(data);
      const result = await (await data).data.data;
      console.log("ini result", result);
      this.form = result;
    },
    async onUpdate(event) {
      event.preventDefault();
      const token = localStorage.getItem("token");
      try {
        const data = await axios.put(
          `http://159.223.57.121:8080/books`,
          this.form,
          {
            headers: {
              Authorization: token,
            },
          }
        );
        console.log("ini update", data);
        alert("data update berhasil");
        this.$router.push("/dashboard");
      } catch (error) {
        alert("data update gagal");
      }
    },
  },
};
</script>
