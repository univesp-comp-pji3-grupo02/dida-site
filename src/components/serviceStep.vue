<template>
  <div>
    <div class="stepper">
      <div class="step">Serviços</div>
      <div class="arrow"><img src="img/icons/right-arrow.svg" alt="right-arrow"></div>
      <div class="circle">2</div>
      <div class="arrow"><img src="img/icons/right-arrow.svg" alt="right-arrow"></div>
      <div class="circle">3</div>
    </div>
    <div class="scheduling-services-container">
      <div
        class="scheduling-services-sub-container"
        v-for="(svc, key) in services"
        :key="key">
        <label
          class="checkbox-container"
          v-if="svc.fixedValue" >
          <input type="checkbox"   :value="svc"
          v-model="selectedServices" />
          {{ svc.name }} — R$ {{ svc.price }}
          <span class="checkmark"></span>
        </label>
        <label
          class="checkbox-container"
          v-else >
          <input type="checkbox"   :value="svc"
          v-model="selectedServices" />
          {{ svc.name }} — A partir de: R$ {{ svc.price }}
          <span class="checkmark"></span>
        </label>
      </div>
    </div>
    <button class="button-prev-next" @click='sendSelectedServices'>Continuar</button>
  </div>
</template>

<script>
export default {
  name: 'ServiceStep',
  props: {
    services: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      selectedServices: []
    }
  },
  methods: {
    sendSelectedServices () {
      this.$emit('selectedServices', this.selectedServices)
      this.$emit('next')
      console.log(this.selectedServices)
      fetch('http://localhost:8000/scheduling', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.selectedServices) // Lista de objetos
      })
        .then(response => response.json())
        .then(data => {
          console.log('Success:', data)
        })
        .catch((error) => {
          console.error('Error:', error)
        })
    }
  }
}
</script>

<style>
.scheduling-services-container{
  background-color: #e0b79f;
  border-radius: 30px;
  padding: 2rem;
}
.scheduling-services-sub-container {
  display: flex;
  justify-content: flex-start; /* Alinha na horizontal à esquerda */
  margin-bottom: 1rem;
}

/* Estilo do checkbox */
.checkbox-container {
  display: flex;
  align-items: center;
  position: relative;
  padding-left: 25px;
  cursor: pointer;
  user-select: none;
  font-size: 16px;
}

.checkbox-container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Caixa visual do checkbox */
.checkmark {
  position: absolute;
  left: 0;
  top: 2px;
  height: 18px;
  width: 18px;
  background-color: #ffffff;
  border-radius: 4px;
}

/* Quando marcado */
.checkbox-container input:checked + .checkmark {
  background-color: #4CAF50;
}

/* Check visual */
.checkmark::after {
  content: "";
  position: absolute;
  display: none;
  left: 6px;
  top: 2px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
}

/* Exibe o check quando marcado */
.checkbox-container input:checked + .checkmark::after {
  display: block;
}

</style>
