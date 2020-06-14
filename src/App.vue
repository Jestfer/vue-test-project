<template>
  <div id="app">
    <v-app>
      <v-app-bar app color="primary" dark id="nav">
        <router-link to="/">Home</router-link>|
        <router-link to="/about">About</router-link>|
        <router-link to="/firstComponent">First Component</router-link>
      </v-app-bar>

      <div class="header-to-view-spacing"></div>

      <router-view />
    </v-app>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  & > * {
    justify-content: space-evenly;
  }
  a {
    font-weight: bold;
    color: #fff;
    text-decoration: none;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
.header-to-view-spacing {
  margin-top: 102px;
}
</style>
