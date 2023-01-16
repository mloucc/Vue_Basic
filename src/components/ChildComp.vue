<script>
export default {
  emits: ["reply"],
  created() {
    this.$emit("reply", "I am from Child!");
  },
  props: {
    pmsg: String,
  },
};
</script>

<template>
  <h2>{{ pmsg || "No props passed yet" }}</h2>
</template>
