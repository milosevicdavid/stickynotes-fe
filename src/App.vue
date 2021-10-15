<template>
  <div id="app">
    <div id="nav">
      <router-link to="/notes">
        <b-button size="is-medium" rounded class="nav-button"
          >Notes</b-button
        ></router-link
      >
      <router-link to="/addnote">
        <b-button size="is-medium" rounded class="nav-button"
          >+ add note</b-button
        ></router-link
      >
    </div>
    <router-view />
  </div>
</template>

<style>
body {
  background-color: #0073ff;
  height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

.nav-button {
  margin: 20px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
