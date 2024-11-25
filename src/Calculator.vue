<template>
<div class="container mt-5">
    <div class="card shadow-lg p-4">
    <h1 class="text-center text-primary mb-4">Calculadora Aritmética</h1>
    <div class="row g-3">
        <!-- Primeiro número -->
        <div class="col-md-4">
        <input
            type="number"
            v-model.number="number1"
            class="form-control"
            placeholder="Digite o 1º número"
        />
        </div>

        <!-- Operação -->
        <div class="col-md-4">
        <select v-model="operation" class="form-select">
            <option value="+">Somar</option>
            <option value="-">Subtrair</option>
            <option value="*">Multiplicar</option>
            <option value="/">Dividir</option>
        </select>
        </div>

        <!-- Segundo número -->
        <div class="col-md-4">
        <input
            type="number"
            v-model.number="number2"
            class="form-control"
            placeholder="Digite o 2º número"
        />
        </div>
    </div>

    <hr class="my-4" />

    <!-- Resultado -->
    <h2 class="text-center text-success">Resultado: {{ result }}</h2>
    </div>
</div>
</template>

<script>
export default {
data() {
    return {
    number1: 0,
    number2: 0,
    operation: '+',
    };
},
computed: {
    result() {
    switch (this.operation) {
        case '+':
        return this.number1 + this.number2;
        case '-':
        return this.number1 - this.number2;
        case '*':
        return this.number1 * this.number2;
        case '/':
        return this.number2 !== 0 ? this.number1 / this.number2 : 'Erro: Divisão por zero';
        default:
        return 'Operação inválida';
    }
    },
},
};
</script>

<style scoped>
.card {
max-width: 600px;
margin: 0 auto;
border-radius: 15px;
background-color: #f8f9fa;
}

input,
select {
height: 50px;
font-size: 18px;
}

h1 {
font-family: 'Roboto', sans-serif;
}

h2 {
font-weight: bold;
}
</style>
