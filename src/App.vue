<script setup>
import Flex from "./components/Flex.vue";
import Mobile from "./components/Mobile.vue";
import DynamicClass from "./components/DynamicClass.vue";
import MEventListener from "./components/MEvenListener.vue";
import FormBinding from "./components/FormBinding.vue";
import Propos_Emit from "./components/Propos_Emit.vue";
import Watcher from "./components/Watcher.vue";
import Select from "./components/Select.vue";
</script>

<template>
  <head>
    <meta charset="utf-8" />
    <!--img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /-->
  </head>

  <main>
    <body>
      <Select />
      <!-- <MEventListener /> -->
      <!-- <FormBinding /> -->
      <!-- <Watcher /> -->
      <!-- <Flex /> -->
      <!-- <Mobile /> -->
      <!-- <DynamicClass /> -->
      <!-- <Propos_Emit /> -->
    </body>
  </main>
</template>

<style>
.logo {
  display: block;
  margin: 0 auto 2rem;
}

#cclo {
  color: yellow;
  font-size: 2em;
  display: flex;
  justify-content: center;
}
</style>
