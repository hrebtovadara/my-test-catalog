<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Каталог товаров:</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
  * {
    box-sizing: border-box;
    font-size: 13px;
    line-height: 16px;
    color: #666;
    font-family: Arial, Helvetica, sans-serif;
    margin: 0;
  }

  * :link {
    text-decoration: none;

    &:hover {
      text-decoration: underline;
    }
  }

  #app {
    font-family: Arial, Helvetica, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }

  #nav {
    padding: 30px;

    a {
      font-size: 30px;
      text-transform: uppercase;
      font-weight: bold;
      color: #2c3e50;
      text-decoration: none;

      &.router-link-exact-active {
        color: #2c3e50;
      }
    }
  }
</style>