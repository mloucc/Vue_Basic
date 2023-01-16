<script>
export default {
  data() {
    return {
      count: 0,
      message: "Hello World",
    };
  },
  methods: {
    myRev() {
      this.message = this.message.split("").reverse().join("");
      console.log("myRev");
    },
  },
};
</script>
<template>
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta charset="utf-8" />
  </head>
  <main>
    <body>
      <button @click="count++">count is: {{ count }}</button>
      <h1>{{ message }}</h1>
      <button @click="myRev">Reverse Message</button>
      <p />
      <button @click="message += '!'">Append "!"</button>
    </body>
  </main>
</template>
