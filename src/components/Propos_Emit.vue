<script>
import ChildComp from "./ChildComp.vue";

export default {
  components: {
    ChildComp,
  },
  data() {
    return {
      greeting: "Hello from parent",
      childMsg: "No child msg yet",
    };
  },
};
</script>

<template>
  <ChildComp :pmsg="greeting"  @reply="(msg) => (childMsg = msg)" />
  <div class="child">{{ childMsg }}</div>
</template>

<style>
.child {
  color: darkgreen;
  font-size: 3em;
}
</style>
