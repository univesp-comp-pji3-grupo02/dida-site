<template>
  <div class="stepper">
    <div class="circle">1</div>
    <div class="arrow">
      <img src="img/icons/right-arrow.svg" alt="right-arrow">
    </div>
    <div class="step">Data</div>
    <div class="arrow">
      <img src="img/icons/right-arrow.svg" alt="right-arrow">
    </div>
    <div class="circle">3</div>
  </div>

  <div class="scheduling-h1"></div>

  <div class="scheduling-container">
    <CalendarGrid @openModal="openModal" @sendFullDate="handleDate" />
  </div>

  <div class="map-key">
    <div class="map-key-item">
      <div id="key-unavailable" class="key"></div>
      <span>Indisponivel</span>
    </div>
    <div class="map-key-item">
      <div id="key-today" class="key"></div>
      <span>Hoje</span>
    </div>
    <div class="map-key-item">
      <div id="key-available" class="key"></div>
      <span>Disponivel</span>
    </div>
  </div>

  <button class="button-prev-next" @click="$emit('prev')">Voltar</button>

  <div class="scheduling-modal">
    <div class="scheduling-modal-container">
      <button @click="closeModal" id="close-modal-button">&times;</button>

      <div class="service-modal">
        <h1>Horarios</h1>
      </div>

      <div class="scheduling-time-modal">
        <button
          class="time"
          v-for="hour in hourTime"
          @click="selectedTime(hour)"
          :key="hour"
          :class="{ selected: timeSelected === hour }"
        >
          {{ hour }}
        </button>
      </div>

      <button class="button-prev-next " @click="notNullNext">Continuar</button>
    </div>
  </div>
</template>

<script>
import CalendarGrid from '@/components/calendar.vue'

export default {
  components: {
    CalendarGrid
  },
  data () {
    return {
      hourTime: ['08:00', '09:00', '10:00', '11:00', '12:00', '13:00', '14:00', '15:00', '16:00', '17:00'],
      timeSelected: null,
      fullDateTime: {}
    }
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
    },
    selectedTime (hour) {
      this.timeSelected = hour
      this.fullDateTime.hour = hour
    },
    notNullNext () {
      if (this.timeSelected === null) {
        alert('selecione um horario')
      } else {
        this.$emit('selectedTime', this.timeSelected)
        this.$emit('next')
        this.$emit('fullDateTimeSelected', this.fullDateTime)
      }
    },
    handleDate (fullDate) {
      this.fullDateTime.date = fullDate
    }
  }
}
</script>
<style>
.selected {
  background-color: #FEFDFD !important;
  color: #000 !important;
}
</style>
