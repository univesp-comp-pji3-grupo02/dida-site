<template>
    <div class="scheduling">
      <div class="scheduling-h1">
        <h1>Agendar atendimento</h1>
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
    </div>
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
      </div>

    </div>
  </template>
<style>
/* general styles */
.scheduling{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}

/* container styles */
.scheduling-container{
  display: flex;
  flex-direction: row;
  gap: 1rem;
  justify-content: center;
  align-items: center;
  max-width: 70%;
  padding: 1rem 2rem;
}
.map-key{
  width: 70%;
  max-width: 70%;
  background-color: #b1533441;
  border-radius: 10px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
}

/* map key styles */
.map-key-item{
  display: flex;
  gap: 1rem;
  justify-content: flex-start;
  align-items: center;
  margin: 0.5rem 0;
  padding: 0 2rem;
}
#key-unavailable{
  background-color: #BA8B7B;
  width: 2rem;
  height: 2rem;
  border-radius: 10px;
}
#key-available{
  background-color: #fff;
  width: 2rem;
  height: 2rem;
  border-radius: 10px;
}
#key-today{
  background-color: #b15334;
  width: 2rem;
  height: 2rem;
  border-radius: 10px;
}

/* modal styles */
.scheduling-modal {
  background-color: rgba(0, 0, 0, 0.719);
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  visibility: hidden;
}

.scheduling-modal-container{
  background-color: #73361b;
  width: 70%;
  height: 70%;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  border-radius: 10px;
}
.scheduling-modal-container button{
  background-color: transparent;
  font-size: 3rem;
  border: none;
  }
#close-modal-button{
  position: absolute;
  top: 0;
  right: 0;
  margin: 0 0.5rem;
  background-color: transparent;
  font-size: 3rem;
  border: none;
}
.service-modal{
  margin: 2rem;
}
.scheduling-time-modal{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  padding: 0 2rem;
}
.scheduling-time-modal span{
  background-color: #BA8B7B;
  color: #fff;
  padding: 1rem;
  border-radius: 10px;
  text-align: center;
  font-size: 1rem;
  color: #000;
  font-weight: bold;
}
</style>
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
