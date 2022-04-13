<template>
  <div>
    <h3>Version 1.0.0</h3>
    <router-link to="/">Go Back</router-link>
  </div>
</template>

<script>
export default {
  name: "About",
  //   inheritAttrs: false, // disable 'non-props' warning
};
</script>

<style scoped>
div {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 4%;
}
</style>