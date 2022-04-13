<template>
  <button
    @click="$emit('toggle-form')"
    :style="{ background: color }"
    class="btn"
  >
    {{ title }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    title: String,
    color: String,
  },
};
</script>