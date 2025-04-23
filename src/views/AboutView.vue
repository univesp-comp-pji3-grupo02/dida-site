<template>
  <div class="about">
    <h1>Sobre Nós</h1>
    <div class="about-text-container">
      <div class="about-header">
        <h2 id="dida-hairdresser" class="about-h2">Dida cabeleleira</h2>
        <img class="photo-round" src="img/icons/dida-photo.png" alt="">
      </div>
      <div class="about-p">
      <p>
        Sou referência em tratamentos de cabelos e estética, proporcionando aos clientes o que há de mais moderno na área da beleza. Você encontra aqui procedimentos mais modernos e sofisticados do mercado para o tratamento e cuidado dos seus cabelos.
      </p>
      <br>
      <p>
        O <strong>Dida Cabeleireira</strong> – Salão de beleza tem como objetivo oferecer os melhores serviços na cidade de Mauá. Nossa missão é promover bem-estar e empoderamento por meio da beleza, levando cuidado e autoestima para todas as mulheres.
      </p>
      <br>
      <p class="about-text-center">
        <strong>Aqui a prioridade é você!</strong>
      </p>
    </div>
    </div>
  </div>
</template>

<style>
.about {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.about-text-container{
  background-color: #e0b79f;
  max-width: 75%;
  border-radius: 30px;
  padding: 1.5rem 0;
}
.about-p{
  max-width: 90%;
  margin: auto;
  font-size: 0.69rem;
}
.about-p p{
  font-size: 0.69rem;
  font-family: "Open Sans", sans-serif;
}

#dida-hairdresser{
  background-color: #aa7259;
  font-size: 1.275rem;
  padding: 0.5rem 1rem;
  font-family: "Archtects Daughter", cursive;
  font-weight: normal;
  max-width: fit-content;
  white-space: nowrap;
}
.about-header{
  display: flex;
  align-items: start;
  justify-content: space-between;
  transform: translate(-5%, 0%);

}
.photo-round{
  border-radius: 50%;
  width: 128px;
  height: 128px;
  border: 2px solid #aa7259;
  transform: translate(20%, -30%);
}
.about-text-container p{
  font-size: 1.2rem;
  margin: 0.5rem;
}
@media screen and (max-width: 500px) {
  .about-text-container{
    margin: auto;
  }
}
@media screen and (max-width: 379px) {
  .about-text-container{
  max-width: 65%;
}
}

</style>
