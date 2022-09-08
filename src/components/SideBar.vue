<template>
  <div class="sidebar">
    <router-link to="/dashboard" class="active">Katalog Buku</router-link>
    <router-link to="/peminjaman">Peminjaman</router-link>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.sidebar {
  width: 200px;
  background-color: #f1f1f1;
  position: fixed;
  /* position: relative; */
  height: 100%;
  overflow: auto;
}
.sidebar a.active {
  background-color: #0b5ed7;
  color: white;
}

.sidebar a {
  display: block;
  color: black;
  padding: 16px;
  text-decoration: none;
}

.sidebar a:hover:not(.active) {
  background-color: #555;
  color: white;
}
</style>
