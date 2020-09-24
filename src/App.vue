<template>
  <div >
  <h1>IMC</h1>

     <label>
      peso
      <input type="text" autofocus @input="addPeso($event.target.value)">
    </label>

      <label>
      altura
      <input type="text" autofocus @input="addAltura($event.target.value)">
    </label>
    <button type="button" @click="caclImc()"> Calcular</button>
       <span> {{error}}</span>

    <p> Seu IMC: {{imc}}</p>
          <div class="container">
        <div >
          <p> Classificação</p>
          <p> IMC</p>
        </div>
        <div  v-bind:class="{ 'active': resultTable === 'abaixo'}">
          <p> Abaixo do peso</p>
          <p> Abaixo de 18.5 </p>
        </div>
        <div  v-bind:class="{ 'active': resultTable === 'normal'}">
          <p> Peso normal</p>
          <p> 18,5 - 24,9 </p>
        </div>
        <div  v-bind:class="{ 'active': resultTable === 'peso'}">
          <p> Sobre Peso</p>
          <p> 25 - 29,9</p>
        </div>
        <div v-bind:class="{ 'active': resultTable === 'grau1'}">
          <p>Obsidade grau I</p>
          <p> 30 - 34,9 </p>
        </div>
        <div v-bind:class="{ 'active': resultTable === 'grau2'}">
          <p>Obsidade grau II</p>
          <p> 35 - 39,9 </p>
        </div>
        <div v-bind:class="{ 'active': resultTable === 'grau3'}">
          <p>Obsidade grau III ou Mórbida</p>
          <p> Maior que 40</p>
        </div>
      </div>

  </div>


</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      peso: '',
      altura: '',
      imc: '',
      error: '',
      resultTable: ''

    }
  },
  methods: {
    addPeso: function(peso) {
  this.error = ''
      this.peso =  parseFloat(peso);

    },
    addAltura: function(altura) {
      this.error = ''
      this.altura =  parseFloat(altura);
    },
    caclImc: function(){
      if(!this.peso || !this.altura) {
        this.error = "Campos vazios";
        return;
      }
      this.imc = (this.peso / (this.altura * this.altura)).toFixed(2)

      if (this.imc < 18.5) {
      this.resultTable = 'abaixo'
    } else if (this.imc > 18.5 && this.imc <= 24.9) {
      this.resultTable = 'normal'
    } else if (this.imc > 24.9 && this.imc <= 29.9) {
      this.resultTable = 'peso'
    } else if (this.imc > 29.9 && this.imc <= 34.9) {
      this.resultTable = 'grau1'
    } else if (this.imc > 34.9 && this.imc <= 39.9) {
      this.resultTable = 'grau2'
    } else if (this.imc > 40) {
      this.resultTable = 'grau3'
    } else {
      this.resultTable = ''
    }
    }
  },
}
</script>

<style>

.container {
  display: flex;
  flex-direction: column;
}
.container div {
  padding: 5px;
  display: flex;
  justify-content: space-around;
}

.container div p {
  padding: 5px;
  margin: 0;
}

.active {
  background-color: #528;
  color: #fff;
  font-weight: 600;
}
</style>
