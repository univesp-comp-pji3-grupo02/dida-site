<template>
    <div class="stepper">
      <div class="circle">1</div>
      <div class="arrow"><img src="img/icons/right-arrow.svg" alt="right-arrow"></div>
      <div class="step">Data</div>
      <div class="arrow"><img src="img/icons/right-arrow.svg" alt="right-arrow"></div>
      <div class="circle">3</div>
    </div>
    <div class="scheduling-h1">
    </div>
    <div class="scheduling-container">
      <CalendarGrid @openModal="openModal" />
    </div>
    <div class="map-key">
      <div class="map-key-item">
        <div id="key-unavailable" class="key"></div><span>Indisponivel</span>
      </div>
      <div class="map-key-item">
        <div id="key-today" class="key"></div><span>Hoje</span>
      </div>
      <div class="map-key-item">
        <div id="key-available" class="key"></div><span>Disponivel</span>
      </div>
    </div>
    <button class="button-prev-next" @click="$emit('prev')" >Voltar</button>
    <div class="scheduling-modal">
      <div class="scheduling-modal-container">
        <button @click="closeModal" id="close-modal-button">&times;</button>
        <div class="service-modal">
          <h1>Serviços</h1>
        </div>
        <div class="scheduling-time-modal">
          <span>08:00</span>
          <span>09:00</span>
          <span>10:00</span>
          <span>11:00</span>
          <span>12:00</span>
          <span>13:00</span>
          <span>14:00</span>
          <span>15:00</span>
          <span>16:00</span>
          <span>17:00</span>
          <span>18:00</span>
          <span>19:00</span>
        </div>
        <button class="button-prev-next" @click="$emit('next')" >Continuar</button>
    </div>
    </div>
</template>
<script>
import CalendarGrid from '@/components/calendar.vue'

export default {
  components: {
    CalendarGrid
  },
  methods: {
    openModal () {
      const modal = document.querySelector('.scheduling-modal')
      modal.style.visibility = 'visible'
      modal.style.opacity = '1'
    },
    closeModal () {
      const modal = document.querySelector('.scheduling-modal')
      modal.style.visibility = 'hidden'
      modal.style.opacity = '0'
    }
  }
}
</script>
