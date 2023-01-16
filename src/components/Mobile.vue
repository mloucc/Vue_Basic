<template>
  <head>
    <meta name="viewport" content="width=device-width, initial-scale= 1.0" />
    <meta charset="utf-8" />
    <!--img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /-->
  </head>

  <main>
    <body>
      <div class="desktop_menu">Menu1, Menu2, Menu3</div>
      <div id="mobile" class="mobile_menu">Moble1, Mobile2, Mobile3</div>

      <div class="list">
        <div class="product">P1</div>
        <div class="product">P2</div>
        <div class="product">P3</div>
        <div class="product">P4</div>
      </div>
    </body>
  </main>
</template>

<style>
.desktop_menu {
  display: flex;
  justify-content: center;
}

.mobile_menu {
  display: none;
  justify-content: center;
}

.list {
  display: flex;
  justify-content: center;
}

.product {
  width: 230px;
  margin: 10px;
  text-align: center;
  background-color: #36d792af;
}

@media (max-width: 1024px) {
  .list {
    flex-wrap: wrap;
  }

  .product {
    width: 40%;
  }
}

@media (max-width: 600px) {
  .desktop_menu {
    display: none;
  }

  .mobile_menu {
    display: flex;
  }

  .list {
    flex-wrap: wrap;
  }

  .product {
    width: 90%;
  }
}
</style>
