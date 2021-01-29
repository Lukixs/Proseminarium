<template>
  <div>
    <b-navbar toggleable="lg" type="light" variant="light" fixed="top">
      <b-navbar-brand to="/"
        >Aplikacja porównojąca czasy wykonwywania dla poszczególnych technologi
        bazodanowych</b-navbar-brand
      >

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "Nav",
  methods: {
    logOut() {
      localStorage.clear();
      this.$router.push("/login");
    },
  },
};
</script>

<style></style>
