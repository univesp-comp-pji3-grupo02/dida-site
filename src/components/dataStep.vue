<template>
    <div class="stepper">
      <div class="circle">1</div>
      <div class="arrow"><img src="img/icons/right-arrow.svg" alt="right-arrow"></div>
      <div class="circle">2</div>
      <div class="arrow"><img src="img/icons/right-arrow.svg" alt="right-arrow"></div>
      <div class="step">Dados</div>
    </div>
    <div class="form-container">
      <label for="nome">Nome</label>
      <input  v-model="userName" type="text" id="nome" name="nome" placeholder="Seu nome" required >
      <label for="phone">Telefone</label>
      <input
    type="tel"
    v-model="userPhone"
    @input="phoneFormat"
    placeholder="(xx) xxxxx-xxxx"
    maxlength="15"
    required
  />
    </div>
    <button class="button-prev-next" @click="getData" >Continuar</button>
    <button class="button-prev-next" @click="$emit('prev')" >Voltar</button>
</template>

<script>
export default {
  name: 'DataStep',
  data () {
    return {
      userData: {},
      userPhone: '',
      userName: ''
    }
  },
  methods: {
    phoneFormat (event) {
      let telefone = event.target.value.replace(/\D/g, '')

      // Limita a 11 dígitos (2 DDD + 9 número)
      telefone = telefone.slice(0, 11)

      if (telefone.length > 10) {
        telefone = telefone.replace(/(\d{2})(\d{5})(\d{4})/, '($1) $2-$3')
      } else if (telefone.length > 6) {
        telefone = telefone.replace(/(\d{2})(\d{4})(\d{0,4})/, '($1) $2-$3')
      } else if (telefone.length > 2) {
        telefone = telefone.replace(/(\d{2})(\d{0,4})/, '($1) $2')
      } else {
        telefone = telefone.replace(/(\d*)/, '($1')
      }

      event.target.value = telefone
    },
    getData () {
      if (this.userName === '' || (this.userPhone === '' || this.userPhone.length < 14)) {
        alert('Preencha todos os campos')
      } else {
        this.userData = {
          userName: this.userName,
          userPhone: this.userPhone
        }
        this.$emit('setUserData', this.userData)
        this.$emit('next')
      }
    }
  }
}
</script>
<style>
.form-container{
  background-color: #BA8B7B;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
  border-radius: 30px;
  margin: 20px;
  width: 80%;
}
.form-container input{
  background-color: #cecece;
  width: 80%;
  height: 2rem;
  border-radius: 10px;
  margin-bottom: 10px;
  border: none;
  color: #000;
  padding: 1rem;
  font-size: 1rem;
}
.form-container input::placeholder{
  color: #7e7e7e;
  font-size: 1rem;
}
.form-container input:focus{
  outline: none;
  background-color: #ffffff;
  }
</style>
