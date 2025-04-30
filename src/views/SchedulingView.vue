<template>
    <div class="scheduling">
      <div class="stepConteiner">
        <component :is="currentStepComponent" @next="nextStep" @prev="prevStep"  @cancel="cancelStep" @postScheduling="postSchedulingDetails"/>
      </div>

    </div>
    </template>
<style>
.button-prev-next{
  font-size: 2rem;
  margin-top: 0.625rem;
  justify-content: center;
  align-content: center;
  align-items: center;
  list-style: none;
  border-radius: 3.1875rem;
  min-width: fit-content;
  background-color: #e0b79f;
  font-family: "Archtects Daughter", cursive;
  padding: 0 1rem;
  border: none;
  color:#9B6F58;
}
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
  height: fit-content;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  border-radius: 10px;
  padding: 1rem 2rem;
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
.stepConteiner{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-family: 'Roboto', sans-serif;
}

#cancel-button{
  margin-top: 2rem;
  font-size: 1.2rem;
}
</style>
<script>
import dateStep from '@/components/dateStep.vue'
import serviceStep from '@/components/serviceStep.vue'
import dataStep from '@/components/dataStep.vue'
import confirmationStep from '@/components/confirmationStep.vue'
export default {
  name: 'SchedulingView',
  components: {
    dateStep,
    serviceStep,
    dataStep
  },
  data () {
    return {
      Services: {
        corte: { price: 50, duration: 30 },
        barba: { price: 30, duration: 20 },
        'corte-barba': { price: 70, duration: 50 },
        'corte-cabelo': { price: 50, duration: 30 },
        'corte-cabelo-barba': { price: 80, duration: 60 },
        'corte-cabelo-barba-sobrancelha': { price: 90, duration: 70 }
      },
      selectedService: null,
      step: 1
    }
  },
  computed: {
    currentStepComponent () {
      return {
        1: serviceStep,
        2: dateStep,
        3: dataStep,
        4: confirmationStep

      }[this.step]
    }
  },
  methods: {
    nextStep () {
      if (this.step < 4) this.step++
    },
    prevStep () {
      if (this.step > 1) this.step--
    },
    cancelStep () {
      this.step = 1
    },
    postSchedulingDetails () {
      this.$router.push('/welcome')
    }
  }
}
</script>
