<template>
  <header>
    <router-link to="/">
      <h1><span>Meetline</span> Movies</h1>
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
  <footer>
    <p>
      Meetline Tech {{ currentYear }}.All rights reserved Made By Eziamaka
      Promise
    </p>
  </footer>
</template>
<script>
export default {
  data() {
    return {
      currentYear: new Date().getFullYear(),
    };
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Fira Sans", sans-serif;
}

body {
  background-color: #35495e;
}

a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #2c3d4e;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
}
h1 {
  color: #fff;
  font-size: 28px;
}
span {
  color: #42b883;
}
footer {
  color: white;
  font-weight: 700;
  font-size: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #2c3d4e;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
  text-align: center;
}
</style>
