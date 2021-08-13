<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Comfortaa:wght@300;400;500;600;700&display=swap');

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  --bg1: #151515;
  --bg2: #252525;
  --done: #6930C3;
  --h1: #64DFDF;
  --p1: #80FFDB;

  background-color: var(--bg1);
  margin: 0;
  padding: 0;
  height: 100vh;
  width: 100vw;

  font-family: "Comfortaa", sans-serif;
}
</style>
