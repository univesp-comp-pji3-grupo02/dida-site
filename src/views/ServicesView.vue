<template>
  <div class="services">
  <h1>Serviços</h1>
    <div class="services-conteiner">
      <div class="services-itens">
        <div class="itens" v-for="(item, index) in itemList" :key="index">{{ item }}</div>
    </div>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      itemList: [
        'Corte',
        'Escovas',
        'Hidratação',
        'Reconstrução',
        'Cauterização',
        'Mechas',
        'Coloração',
        'Tonalização',
        'Selagem',
        'Penteados',
        'Cronograma Capilar',
        'Progressiva',
        'Mega Hair'
      ]
    }
  }
}
</script>
<style>
.services{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.services-conteiner{
  max-width: 90%;
}
.itens{
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #aa7259;
  width: 105px;
  height: 55px;
  border-radius: 7px;
  color: #fff;
  font-family: "Archtects Daughter", cursive;
  font-size: 1rem;
  font-weight: bold;
}
.services-itens{
width: 70%;
display: grid;
column-gap: 1rem;
row-gap: 1rem;
grid-template-columns: repeat(3, 1fr);

}
</style>
