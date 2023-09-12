
<script setup lang="ts">

import { reactive } from 'vue';
import { OPERACOES } from './constants/operacoes'

const MAIOR_OPERADOR = 0

const state = reactive({ numero: "", expressao: "", total: 0 })

function adicionarOperador(operador: number | string): void {
    state.expressao = state.expressao + String(operador)
}

function handleSubmit(): void {
    state.expressao = eval(state.expressao)
}

</script>

<template>
    <div class="calculadora">
        <div class="expressao">
            {{ state.expressao }}
        </div>
        <div class="operadores">
            <button @click="adicionarOperador(numero)" v-for="numero in OPERACOES"
                :class="numero === MAIOR_OPERADOR ? 'botao-maior' : 'botao'" type="button">
                {{ numero }}
            </button>
        </div>
        <button class="submit" @click="handleSubmit">
            SOMAR
        </button>
    </div>
</template>

<style>
.calculadora {
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.expressao {
    max-width: 392px;
    width: 100%;
    height: 32px;
    margin-bottom: 16px;
    font-size: 1.25rem;
    text-align: right;
    padding: 6px;
    border-radius: 8px;
    background-color: #1a1a1a;
}

.operadores {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 8px;
    max-width: 400px;
    width: 100%;

}

.botao,
.botao-maior {
    display: flex;
    justify-content: center;
}

.botao-maior {
    grid-column-start: 1;
    grid-column-end: 3;
}

.submit {
    width: 100%;
    max-width: 400px;
    margin-top: 16px;
    display: flex;
    justify-content: center;
}
</style>
