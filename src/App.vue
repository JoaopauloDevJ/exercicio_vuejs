<script setup>
import { ref, watch } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
  
let soma = ref({
  numero1: 0,
  numero2: 0,
})

const valor = ref({
  filtro: 'somar',
})

  function resultadoSomar() {
  return soma.value.numero1 + soma.value.numero2;
}

  const resultadoSubtrair = () => {
    return soma.value.numero1 - soma.value.numero2;
  }

  const resultadoDivisao = () => {
    return soma.value.numero1 / soma.value.numero2;
  }

  const resultadoMultiplicar = () => {
    return soma.value.numero1 * soma.value.numero2;
  }

  const getValorAritmetico = () => {
    const {filtro} = valor.value;

    switch(filtro) {
      case 'somar':
        return resultadoSomar();
      case 'subtrair':
        return resultadoSubtrair();
      case 'divisao':
        return resultadoDivisao();
      default:
        return resultadoMultiplicar();
    }
  }

  const resultado = ref(getValorAritmetico());
  watch(soma, () => {
    resultado.value = getValorAritmetico();
  })

</script>

<template>
  <div class="container">
    <Cabecalho/>
    <div class="row mt-5 calculadora">
      <div class="col-md-3">
          <input v-model="soma.numero1" type="number" class="form-control" placeholder="Digite um numero:"/>
      </div>
      <div class="col-md-1">
          <select v-model="valor.filtro" class="form-control">
          <option value='somar'>+</option>
          <option value='subtrair'>-</option>
          <option value='divisao'>/</option>
          <option value='multiplicar'>*</option>
          </select>
      </div>
      <div class="col-md-3">
          <input v-model="soma.numero2" type="number" class="form-control" placeholder="Digite um numero:"/>
      </div>
      <div class="col">
          <p> {{ getValorAritmetico() }} </p>
      </div>
    </div>
  </div>
</template>

