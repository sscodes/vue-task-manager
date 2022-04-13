<template>
  <footer>
    <h4>Copyright &copy; 2022</h4>
    <router-link to="/about" v-show="homePage">About</router-link>
  </footer>
</template>

<script>
export default {
  name: "Footer",
  computed: {
    homePage() {
      if (this.$route.path === "/") return true;
      return false;
    },
  },
};
</script>

<style>
a {
  color: #333;
}

footer {
  margin-top: 30px;
  text-align: center;
}
</style>