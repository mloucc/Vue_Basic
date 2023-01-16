<script>
export default {
  data() {
    return {
      titleClass: "title",
    };
  },
};
</script>
<template>
  <meta name="viewport" content="width=device-width, initial-scale = 1.0 " />
  <meta charset="utf-8" />
  <main>
    <body>
      <h3 :class="titleClass">Change Color</h3>
    </body>
  </main>
</template>

<style>
.title {
  color: red;
}
.item {
  color: greenyellow;
}
</style>
