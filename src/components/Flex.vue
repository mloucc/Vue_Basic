<template>
  <div class="mflex">
    <div class="left">hello</div>
    <div class="right">welcome</div>
  </div>
</template>

<style>
.mflex {
  display: flex;
}

.left {
  background-color: aqua;
  flex: none;
  width: 200px;
}

.right {
  background-color: greenyellow;
  display: flex;
  flex: auto;
  justify-content: flex-end;
}
</style>
