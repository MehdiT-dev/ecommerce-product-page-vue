<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view/>
</template>

<style lang="scss">
// Reset CSS
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-size: 0.85em;
}

#app {
  font-family: 'Kumbh Sans', Helvetica, Arial, sans-serif;
  font-size: 1.1em;
  // -webkit-font-smoothing: antialiased;
  // -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  // color: #2c3e50;
}

nav {
  // padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
