<template>
  <div id="app">
    <nav class="nav-icons nav-top-icons">
        <div class="nav-top-icons-left-buttons">
          <button id="home-button" @click="isMenuOpen = true">
            <img class="home-icon-filter" src="img/icons/bars-menu-icon.svg" alt="home button">
          </button>
        </div>
        <div class="nav-top-icons-right-buttons">
          <button class="home-icon-filter" id="back-button">
            <img src="img/icons/back-icon.svg" alt="back button">
          </button>
          <button id="refresh-button">
            <img class="home-icon-filter" src="img/icons/refresh-icon.svg" alt="refresh button">
          </button>
        </div>

      </nav>
      <div class="nav-side-menu" v-if="isMenuOpen">
        <NavMenu @close-nav="isMenuOpen = false" />
      </div>

    <DidaLogo />
    <router-view />

    <footer>
      <p>© 2023 Dida. Todos os direitos reservados.</p>
      <p>Desenvolvido por <a href="#">PJI 310-sala 005 grupo 022 </a></p>
    </footer>
  </div>
</template>

<script>
import { ref } from 'vue'
import DidaLogo from './components/InitialLogo.vue'
import NavMenu from './components/navMenu.vue'

export default {
  name: 'App',
  components: {
    DidaLogo,
    NavMenu
  },
  setup () {
    const isMenuOpen = ref(false)
    return { isMenuOpen }
  }
}
</script>

<style>
/* Reset e base */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Archtects Daughter", cursive;
}

body {
  background-color: #e4ccc2;
  font-family: "Archtects Daughter", cursive;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 0;
}

a {
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #9B6F58;
}

/* Componentes principais */
.nav-icons {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.nav-top-icons {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  background-color: #dcaf95;
  width: 100%;
  padding: 0 2rem;
}

.nav-top-icons-left-buttons {
  display: flex;
  margin-left: 2rem;
  justify-content: flex-start;
}

.nav-top-icons-right-buttons {
  display: flex;
  width: fit-content;
  margin: 0;
  justify-content: flex-end;
  flex-grow: 1;
  margin-right: 2rem;
}

.nav-top-icons button {
  background-color: transparent;
  border: none;
  cursor: pointer;
  margin: 0.5rem;
}

.nav-list {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

footer {
  margin: 2rem auto;
}

h1 {
  margin-bottom: 1.5rem;
  font-size: 2rem;
  margin-top: 0.625rem;
  justify-content: center;
  align-content: center;
  align-items: center;
  list-style: none;
  border-radius: 3.1875rem;
  width: 20.6875rem;
  height: 3.9375rem;
  min-width: fit-content;
  background-color: #e0b79f;
  font-family: "Archtects Daughter", cursive;
  font-weight: normal;
  padding: 0 1rem;
}

.home-icon-filter {
  filter: brightness(0) saturate(100%) invert(28%) sepia(81%) saturate(566%) hue-rotate(5deg) brightness(94%) contrast(94%);
}

/* Media queries */
@media screen and (max-width: 500px) {
  nav {
    padding: 1.9rem;
  }

  .nav-list ul {
    list-style: none;
    display: flex;
  }

  .nav-list li {
    font-size: 2rem;
    margin: 0.6rem auto 3rem;
    justify-content: center;
    align-content: center;
    list-style: none;
    border-radius: 51px;
    width: 15rem;
    height: 4rem;
    background-color: #e0b79f;
  }

  h1 {
    width: 75%;
  }
}

@media screen and (max-width: 379px) {
  .about-text-container {
    max-width: 65%;
  }

  h1 {
    font-size: 2rem;
    width: 65%;
  }
}
</style>
