<template>
  <div>
    <b-navbar toggleable="sm" type="light" variant="light" class="p-4">
      <div class="container">
        <b-navbar-toggle target="nav-text-collapse"></b-navbar-toggle>

        <b-navbar-brand>Mega Giga</b-navbar-brand>

        <div class="h3">
          <b-icon icon="person-fill"></b-icon>
          <b-dropdown id="dropdown-1" variant="light">
            <b-dropdown-item>Change Password</b-dropdown-item>
            <b-dropdown-item @click="handleLogout">Logout</b-dropdown-item>
          </b-dropdown>
        </div>
      </div>
    </b-navbar>
  </div>
</template>

<script>
export default {
  methods: {
    handleLogout() {
      localStorage.clear();
      this.$router.push("/");
      location.reload();
    },
  },
};
</script>

<style lang="scss" scoped></style>
