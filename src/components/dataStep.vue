<template>
    <H1>DADOS</H1>
    <button class="button-prev-next" @click="$emit('next')" >Continuar</button>
    <button class="button-prev-next" @click="$emit('prev')" >Voltar</button>
</template>

<script>
export default {
  name: 'DataStep'
}
</script>
