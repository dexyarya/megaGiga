<template>
  <div>
    <!-- <NavBar /> -->
    <ListBook />
  </div>
</template>

<script>
import ListBook from "@/components/ListBook.vue";
// import NavBar from "@/components/NavBar.vue";
export default {
  name: "Dashboard",
  components: {
    ListBook,
    // NavBar,
  },
};
</script>

<style lang="scss" scoped></style>
