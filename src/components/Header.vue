<template>
  <header>
    <h1>{{ title }}</h1>
    <div>
      <Button
        v-show="homePage"
        @toggle-form="$emit('toggle-form')"
        :title="showAddTask ? 'Close' : 'Add Task'"
        color="blue"
      />
    </div>
  </header>
</template>

<script>
import Button from "./Button.vue";

export default {
  name: "Header",
  props: {
    title: {
      type: String,
      default: "Task Tracker",
    },
    showAddTask: {
      type: Boolean,
    },
  },
  components: {
    Button,
  },
  emits: ["toggle-form"],
  computed: {
    homePage() {
      if (this.$route.path === "/") return true;
      return false;
    },
  },
};
</script>

<style scoped>
header {
  display: flex;
  align-items: center;
}
header div {
  margin-right: 0;
  margin-left: auto;
}
</style>