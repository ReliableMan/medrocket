<template>
  <div id="app">
    <nav>
      <router-link to="/">Каталог</router-link> 
      <router-link to="/favorites">Избранное</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin: 64px 204px 0 204px;
}

nav {
  display: flex;
  justify-content: center;
  align-items: center;

  a {
    width: 372px;
    padding: 16px 32px;
    gap: 8px;
    display: flex;
    justify-content: center;
    align-items: center;
    text-decoration: none;
    font-style: normal;
    font-weight: 400;
    font-size: 18px;
    line-height: 130%;
    color: black;

    &.router-link-exact-active {
      background: #EDF9FF;
      border-radius: 16px;
      color: #117DC1;
    }
  }
}
</style>
