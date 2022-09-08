<template>
  <div class="container mt-5">
    <!-- <FormAdd/> -->

    <div class="Title-top d-flex justify-content-between mb-5">
      <router-link :to="{ name: 'formadd' }">
        <b-button variant="primary">Tambah</b-button>
      </router-link>
      <!-- <p class="h4">User List</p> -->
      <div>
        <b-form-input v-model="text" type="search" placeholder="Search">
        </b-form-input>
      </div>
    </div>

    <div class="card">
      <b-table :items="items" :fields="fields" responsive class="text-justify">
        <template #cell(no)="data">
          {{ data.index + 1 }}
        </template>
        <template v-slot:cell(actions)="data">
          <router-link :to="{ name: 'formedit', params: { id: data.item.id } }">
            <b-button size="sm" class="mr-2" variant="warning" title="Edit">
              Edit
            </b-button>
          </router-link>

          <b-button
            size="sm"
            v-on:click="deleteUser(data.item.id)"
            class="mr-2"
            variant="danger"
            title="Delete"
          >
            Hapus
          </b-button>
        </template>
      </b-table>
    </div>
  </div>
</template>

<script>
// import FormAdd from "./FormAdd.vue";
import axios from "axios";
export default {
  components: {
    // FormAdd
  },
  data() {
    return {
      fields: [
        "no",
        "title",
        "isbn",
        "publisher",
        "description",
        { key: "actions", label: "Action" },
      ],

      items: [],
    };
  },
  created() {},
  mounted() {
    this.getData();
  },

  methods: {
    async getData() {
      const token = localStorage.getItem("token");
      axios
        .get("http://159.223.57.121:8080/books?limit=20&offset=0", {
          headers: {
            Authorization: token,
          },
        })
        .then((res) => {
          console.log(res.data.data);
          this.items = res.data.data;

          console.log(this.items);
        });

      console.log(data);
    },

    deleteUser(item) {
      const token = localStorage.getItem("token");

      axios
        .delete(`http://159.223.57.121:8080/books/${item}`, {
          headers: {
            Authorization: token,
          },
        })
        .then(() => {
          // this.$swal({
          //   toast: true,
          //   position: "top-end",
          //   showConfirmButton: false,
          //   timer: 3000,
          //   icon: "success",
          //   text: "User has been deleted",
          // });

          this.getData();
        })
        .catch((error) => {
          console.log(error.data);
        });
    },
  },
};
</script>
