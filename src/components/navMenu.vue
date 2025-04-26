<template>
  <div class="home">
    <a href="javascript:void(0)" class="closebtn" @click="$emit('close-nav')">&times;</a>
    <ul class="nav-list">
      <li @click="$emit('close-nav')">
        <router-link to="/welcome">Boas Vindas</router-link>
      </li>
      <li @click="$emit('close-nav')">
        <router-link to="/about">Sobre Nós</router-link>
      </li>
      <li @click="$emit('close-nav')">
        <router-link to="/services">Serviços</router-link>
      </li>
      <li @click="$emit('close-nav')">
        <router-link to="/scheduling">Agendamento</router-link>
      </li>
      <li @click="$emit('close-nav')">
        <router-link to="/contact">Contatos</router-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'NavMenu'
}
</script>

<style>
.home{
  background-image: url(../../public/img/wall-texture.png);
  background-repeat: no-repeat;
  background-size: cover;
  width: 100%;
  height: 100vh;
  position: fixed;
  z-index: 1;
  top: 0;
  left: 0;
  overflow-x: hidden;
  transition: 0.5s;
  padding-top: 60px;
}
.nav-list li{
margin-bottom: 1.2rem;
}
.nav-list a{
  color: #000;
  font-family: "Archtects Daughter", cursive;
  font-size: 2rem;
  }
  .closebtn{
    position: absolute;
  top: 0;
  right: 25px;
  font-size: 48px;
  margin-left: 50px;
  }
</style>
