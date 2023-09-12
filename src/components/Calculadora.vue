<script setup>
import { reactive, ref, watchEffect } from 'vue';

const estado = reactive({
    filtro: 'soma',
    numeroA: ref(0),
    numeroB: ref(0),
    resultado: ref(0),
});

const operacoes = {
    soma: (a, b) => a + b,
    subtracao: (a, b) => a - b,
    multiplicacao: (a, b) => a * b,
    divisao: (a, b) => {
        if (b === 0) {
            return 'Erro: divisão por zero';
        }
        return a / b;
    },
};

watchEffect(() => {
    const { filtro, numeroA, numeroB } = estado;
    estado.resultado = operacoes[filtro](numeroA, numeroB);
});
</script>

<template>
    <main>
        <form>
            <div class="row">
                <div class="col-md-3">
                    <input v-model="estado.numeroA" type="number" class="form-control"
                        placeholder="Digite o primeiro número">
                </div>
                <div class="col-md-3">
                    <input v-model="estado.numeroB" type="number" class="form-control" placeholder="Digite o segundo número">
                </div>
                <div class="col-md-2 mb-10">
                    <select v-model="estado.filtro" class="form-select">
                        <option value="soma" selected>Soma</option>
                        <option value="subtracao">Subtração</option>
                        <option value="multiplicacao">Multiplicação</option>
                        <option value="divisao">Divisão</option>
                    </select>
                </div>
            </div>
        </form>
        <div class="row mt-3">
            <div class="col-md-2">
                <span class="form-control">Resultado: {{ estado.resultado }}</span>
            </div>
        </div>
    </main>
</template>

<style scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}
</style>