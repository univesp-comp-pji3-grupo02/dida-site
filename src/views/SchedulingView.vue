<template>
    <div class="scheduling">
      <div class="stepConteiner">
        <component
        :is="currentStepComponent"
        @next="nextStep"
        @prev="prevStep"
        @postScheduling="postSchedulingDetails"
        @selectedServices="handleSelectedServices"
        @fullDateTimeSelected="handleDate"
        @setUserData="handleUserData"
        :services="services"
        :dataScheduling="dataScheduling"
      />
      </div>
    </div>
</template>
<style>

.button-prev-next {
  cursor: pointer;
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
  color: #9B6F58;
  transition: all 0.3s ease-in-out;
}
.button-prev-next:hover {
  color: #744e3a;
}
.scheduling {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.stepConteiner {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-family: 'Roboto', sans-serif;
}

.scheduling-container {
  display: flex;
  flex-direction: row;
  gap: 1rem;
  justify-content: center;
  align-items: center;
  max-width: 70%;
  padding: 1rem 2rem;
}

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

.scheduling-modal-container {
  background-color: #E0B79F;
  width: 70%;
  height: fit-content;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  border-radius: 30px;
  padding: 1rem 2rem;
}

.service-modal {
  margin: 2rem;
}

.scheduling-time-modal {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
  padding: 0 2rem;
}

.scheduling-time-modal button {
  background-color: #E6C5B2;
  color: #000;
  padding: 0.5rem 2rem;
  border-radius: 20px;
  text-align: center;
  font-size: 1rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
  border: none;
  cursor: pointer;
}
.scheduling-time-modal button:hover {
  background-color: #e0b79f;
}

#cancel-button {
  margin-top: 2rem;
  font-size: 1.2rem;
}

#close-modal-button {
  position: absolute;
  top: 0;
  right: 0;
  margin: 0 0.5rem;
  background-color: transparent;
  font-size: 3rem;
  border: none;
}

.map-key {
  width: 70%;
  max-width: 70%;
  background-color: #b1533441;
  border-radius: 10px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
}

.map-key-item {
  display: flex;
  gap: 1rem;
  justify-content: flex-start;
  align-items: center;
  margin: 0.5rem 0;
  padding: 0 2rem;
}

#key-unavailable {
  background-color: #BA8B7B;
  width: 2rem;
  height: 2rem;
  border-radius: 10px;
}

#key-available {
  background-color: #fff;
  width: 2rem;
  height: 2rem;
  border-radius: 10px;
}

#key-today {
  background-color: #b15334;
  width: 2rem;
  height: 2rem;
  border-radius: 10px;
}
.stepper {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 20px;
    }

    .step {
      background-color: #a36f57; /* cor da bolha "Serviços" */
      color: black;
      font-weight: bold;
      padding: 10px 20px;
      border-radius: 999px;
    }

    .circle {
      background-color: #e5bda5;
      color: black;
      font-weight: bold;
      width: 40px;
      height: 40px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .arrow {
      height: 20px;
      width: 20px;
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
    dataStep,
    confirmationStep
  },
  data () {
    return {
      services: {
        avaliacao: {
          id: 0,
          name: 'Avaliação',
          price: 0,
          duration: 10,
          fixedValue: true
        },
        corte: {
          id: 1,
          name: 'Corte',
          price: 40,
          duration: 30,
          fixedValue: true
        },
        tratamentos: {
          id: 2,
          name: 'Tratamentos',
          price: 120,
          duration: 60,
          fixedValue: false
        },
        coloracao: {
          id: 3,
          name: 'Coloração',
          price: 150,
          duration: 90,
          fixedValue: false
        },
        quimica: {
          id: 4,
          name: 'Química em Geral',
          price: 180,
          duration: 120,
          fixedValue: false
        },
        depilacaoCompleta: {
          id: 5,
          name: 'Depilação Completa',
          price: 140,
          duration: 60,
          fixedValue: true
        },
        depilacaoVirilha: {
          id: 6,
          name: 'Depilação Virilha',
          price: 60,
          duration: 20,
          fixedValue: true
        },
        depilacaoAxila: {
          id: 7,
          name: 'Depilação Axila',
          price: 30,
          duration: 15,
          fixedValue: true
        },
        depilacaoPernaInteira: {
          id: 8,
          name: 'Depilação Perna Inteira',
          price: 60,
          duration: 30,
          fixedValue: true
        },
        depilacaoMeiaPerna: {
          id: 9,
          name: 'Depilação Meia Perna',
          price: 30,
          duration: 20,
          fixedValue: true
        },
        depilacaoBuco: {
          id: 10,
          name: 'Depilação Buço',
          price: 20,
          duration: 10,
          fixedValue: true
        },
        sobrancelha: {
          id: 11,
          name: 'Sobrancelha',
          price: 30,
          duration: 15,
          fixedValue: true
        },
        terapiaCapilar: {
          id: 12,
          name: 'Terapia Capilar',
          price: 150,
          duration: 60,
          fixedValue: false
        },
        escova: {
          id: 13,
          name: 'Escova',
          price: 50,
          duration: 45,
          fixedValue: false
        },
        hidratacao: {
          id: 14,
          name: 'Hidratação',
          price: 80,
          duration: 45,
          fixedValue: true
        }
      },
      step: 1,
      dataScheduling: {
        serviceScheduling: {},
        dateScheduling: {},
        userData: {}
      }
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
      if (this.step < 5) this.step++
    },
    prevStep () {
      if (this.step > 1) this.step--
    },
    postSchedulingDetails () {
      alert('Agendamento realizado com sucesso!')
      this.$router.push('/welcome')
    },
    handleSelectedServices (selectedServices) {
      const temporarylyList = []
      for (const service of selectedServices) {
        temporarylyList.push(service)
      }
      this.dataScheduling.serviceScheduling = temporarylyList
    },
    handleDate (date) {
      this.dataScheduling.dateScheduling = date
    },
    handleUserData (userData) {
      this.dataScheduling.userData = userData
    }
  }
}
</script>
