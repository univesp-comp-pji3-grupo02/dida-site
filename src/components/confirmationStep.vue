<template>
<div class="confirmation-text-container">
    <h1>Confirme seu agendamento </h1>
    <h2><img src="img/icons/scissorsIcon.svg" alt="icon of a calendar" class="svgIcons"> Por favor, revise os dados abaixo antes de finalizar: </h2>
    <br>
    <p><strong><img src="img/icons/calendarIcon.svg" alt="icon of a calendar" class="svgIcons"> Data:</strong> {{formatDate(dataScheduling.dateScheduling.date)}}</p>
    <p><strong><img src="img/icons/clockIcon.svg" alt="icon of a clock" class="svgIcons"> Horario:</strong> {{dataScheduling.dateScheduling.hour}}</p>
    <p><strong><img src="img/icons/briefCaseIcon.svg" alt="icon of a briefcase" class="svgIcons"> Serviços:</strong> </p>

    <ul>
        <li v-for="(service, index) in dataScheduling.serviceScheduling"
            :key="index">
            {{ service.name }} -
            <span v-if="service.fixedValue">R${{ service.price }}</span>
            <span v-else>A partir de R${{ service.price }}</span>
        </li>
    </ul>

    <p><strong><img src="img/icons/cashIcon.svg" alt="icon of a money bill" class="svgIcons"> Valor estimado:</strong> a partir de R$ {{calculatePrice}}</p>
</div>
<button class="button-prev-next" @click="SchedulingComplete" >Agendar</button>
<button id="cancel-button" class="button-prev-next" @click="$emit('prev')" >cancelar</button>
</template>

<style>
.svgIcons{
  width: 1rem;
  height: 1rem;
  filter: brightness(0) saturate(100%) invert(28%) sepia(81%) saturate(566%) hue-rotate(5deg) brightness(94%) contrast(94%);
}
.confirmation-text-container{
    color: #9B6F58;
    display: flex;
    flex-direction: column;
    text-align: left;
    background-color: #e0b79f;
    max-width: 80%;
    border-radius: 30px;
    padding: 1.5rem 1rem;
}
.confirmation-text-container ul{
    list-style: none;
    padding-left: 0;
}
.confirmation-text-container li{
    margin: 1rem;
}
.confirmation-text-container h1,h2{
    font-weight: bold;
    font-family: "Archtects Daughter", cursive;
    text-align: center;
}
.confirmation-text-container h2{
    font-weight: regular;
    font-size: 1rem;
}
.confirmation-text-container h1 {
    padding: 0;
    font-size: 1.5rem;
    white-space: nowrap;
    margin: 0 auto;
}

</style>

<script>
export default {
  name: 'ConfirmationStep',
  props: {
    dataScheduling: {
      type: Object,
      required: true
    }
  },
  computed: {
    calculatePrice () {
      let totalService = 0
      for (const service of this.dataScheduling.serviceScheduling) {
        totalService += service.price
      }
      return totalService
    }
  },
  methods: {
    SchedulingComplete () {
      this.$emit('postScheduling')
    },
    formatDate (data) {
      let newData = data.split('-')
      const year = newData[0]
      const month = newData[1]
      const day = newData[2]
      newData = `${day}/${month}/${year}`
      console.log(newData)
      return newData
    }
  }
}
</script>
