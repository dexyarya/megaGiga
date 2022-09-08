<template>
  <div id="app">
    <div v-if="token">
      <NavBar />
      <SideBar />
    </div>
    <router-view />
  </div>
</template>

<script>
import NavBar from "../src/components/NavBar.vue";
import SideBar from "../src/components/SideBar.vue";

export default {
  name: "Dashboard",
  components: {
    NavBar,
    SideBar,
  },

  data() {
    return {
      token: false,
    };
  },

  computed: {
    cektoken() {
      return (this.token = localStorage.getItem("token"));
    },
  },

  created() {
    console.log("ini token", this.cektoken);

    if (cektoken !== "") {
      this.token === true;
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */

  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
