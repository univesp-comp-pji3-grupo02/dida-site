<template>
  <div class="home">
    <ul class="nav-list">
    <li><router-link to="/welcome">Boas Vindas</router-link></li>
    <li><router-link to="/about">Sobre Nós</router-link></li>
    <li><router-link to="/services">Serviços</router-link></li>
    <li><router-link to="/scheduling">Agendamento</router-link></li>
    <li><router-link to="/contact">Contatos</router-link></li>
  </ul>
  <router-view/>
  </div>
</template>
<style>
.nav-list li{
margin-bottom: 1.2rem;
}
.nav-list a{
  color: #000;
  font-family: "Archtects Daughter", cursive;
  font-size: 2rem;
  }
</style>
