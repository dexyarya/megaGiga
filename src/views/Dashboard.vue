<template>
  <div>
    <!-- <NavBar /> -->
    <!-- <SideBar /> -->
    <ListBook />
  </div>
</template>

<script>
import ListBook from "@/components/ListBook.vue";
// import NavBar from "@/components/NavBar.vue";
import SideBar from "@/components/SideBar.vue";
export default {
  name: "Dashboard",
  components: {
    ListBook,
    // NavBar,
    SideBar,
  },
};
</script>

<style lang="scss" scoped></style>
