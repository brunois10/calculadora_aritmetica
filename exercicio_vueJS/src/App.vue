<script setup>

  import { reactive, watch } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';

const estado = reactive({
    filtro: 'soma',
    valorA: 0,
    valorB: 0,
    resultado: 0,
});

function calcular() {
    let { filtro } = estado;

    switch(filtro) {
        case 'soma':
            return estado.resultado = Number(estado.valorA) + Number(estado.valorB);
        case 'subtracao':
            return estado.resultado = Number(estado.valorA) - Number(estado.valorB);
        case 'multiplicacao':
            return estado.resultado = Number(estado.valorA) * Number(estado.valorB);
        case 'divisao':
            return estado.resultado = Number(estado.valorA) / Number(estado.valorB);
        default:
            estado.resultado = 0;
    }
}

watch([() => estado.valorA, () => estado.valorB, () => estado.filtro], () => {
    calcular();
});

</script>

<template>
  <div class="container">
        <Cabecalho />
        <form>
            <div class="row">
                <div class="col-md-2">
                    <select @change="evento => estado.filtro = evento.target.value" class="form-control">
                        <option value="soma">Soma</option>
                        <option value="subtracao">Subtração</option>
                        <option value="multiplicacao">Multiplicação</option>
                        <option value="divisao">Divisão</option>
                    </select>
                </div>
                <div class="col">
                    <input type="text" placeholder="Digite um valor" class="form-control" @keyup="evento => estado.valorA = evento.target.value">
                </div>
                <div class="col">
                    <input type="text" placeholder="Digite outro valor" class="form-control" @keyup="evento => estado.valorB = evento.target.value">
                </div>
                <div class="col-md-2">
                    <button type="submit" class="btn btn-primary">Calcular</button>
                </div>
            </div>
            <div class="row">
                <div class="col-md-6 mt-5">
                    <p>
                        O resultado é: {{ estado.resultado }}
                    </p>
                </div>
            </div>
        </form>
    </div>
</template>

<style scoped>
/* Foi utilizado o bootstrap */
</style>
