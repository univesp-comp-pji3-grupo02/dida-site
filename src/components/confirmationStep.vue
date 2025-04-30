<template>
<H1>Confirmar agendamento</H1>
<div class="confirmation-text-container">
    <h1>Confirme seu agendamento</h1>
    <h2>Por favor, revise os dados abaixo antes de finalizar:</h2>
    <p>Data: [data escolhida]</p>
    <p>Horario: [horario escolhida]</p>
    <p>Serviços: </p>
    <ul>
        <li>Corte - a partir de R$40,00</li>
        <li> Hidratação - R$80,00</li>
    </ul>
    <p>Valor estimado: a partir deR$120,00</p>
</div>
<button class="button-prev-next" @click="$emit('postScheduling')" >Agendar</button>
<button id="cancel-button" class="button-prev-next" @click="$emit('cancel')" >cancelar</button>
</template>

<style>
.confirmation-text-container{
  background-color: #e0b79f;
  max-width: 75%;
  border-radius: 30px;
  padding: 1.5rem 0;
}
</style>

<script>
export default {
  name: 'ConfirmationStep'
}
</script>
