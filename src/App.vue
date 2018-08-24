<template>
  <div id="app">
    <header>
      <ul>
        <router-link tag="li" to="/"><a>Home</a></router-link>
        <router-link tag="li" to="/about"><a>About</a></router-link>
        <router-link tag="li" to="/game"><a>Game</a></router-link>
      </ul>
    </header>

    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

li {
  list-style-type: none;
}

header {
  position: fixed;
  top: 0;
  height: 40px;
  width: 100%;
  border-bottom: 1px solid green;
}

header li {
  float: left;
  margin-right: 20px;
}
</style>
