<template>
    <div class="scheduling">
      <div class="scheduling-h1">
        <h1>Agendar atendimento</h1>
      </div>
      <div class="scheduling-container">
      <CalendarGrid/>
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
  </template>
<style>
.scheduling{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}
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
</style>
<script>
import CalendarGrid from '@/components/calendar.vue'
export default {
  components: {
    CalendarGrid
  }
}
</script>
