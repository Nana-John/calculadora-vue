<template>
<div class="calculator-container">
    <!-- Display da calculadora -->
    <div class="calculator-display">
    {{ currentInput || result || "0" }}
    </div>

    <!-- Botões da calculadora -->
    <div class="calculator-buttons">
    <!-- Números -->
    <button v-for="n in numbers" :key="n" @click="appendNumber(n)" class="btn btn-number">
        {{ n }}
    </button>

    <!-- Operações -->
    <button v-for="op in operations" :key="op" @click="selectOperation(op)" class="btn btn-operation">
        {{ op }}
    </button>

    <!-- Funções especiais -->
    <button @click="clear" class="btn btn-special">C</button>
    <button @click="calculate" class="btn btn-equals">=</button>
    </div>
</div>
</template>

<script>
export default {
data() {
    return {
    currentInput: "", // Número sendo digitado
    previousInput: null, // Número anterior
    operation: null, // Operação selecionada
    result: null, // Resultado final
    };
},
computed: {
    numbers() {
    return [1, 2, 3, 4, 5, 6, 7, 8, 9, 0];
    },
    operations() {
    return ["+", "-", "*", "/"];
    },
},
methods: {
    appendNumber(num) {
    if (this.currentInput.length < 10) {
        this.currentInput += num;
    }
    },
    selectOperation(op) {
    if (this.currentInput === "") return;
    this.previousInput = this.currentInput;
    this.operation = op;
    this.currentInput = "";
    },
    calculate() {
    const prev = parseFloat(this.previousInput);
    const current = parseFloat(this.currentInput);

    if (isNaN(prev) || isNaN(current)) return;

    switch (this.operation) {
        case "+":
        this.result = prev + current;
        break;
        case "-":
        this.result = prev - current;
        break;
        case "*":
        this.result = prev * current;
        break;
        case "/":
        this.result = current !== 0 ? prev / current : "Erro";
        break;
    }

    this.previousInput = null;
    this.operation = null;
    this.currentInput = "";
    },
    clear() {
    this.currentInput = "";
    this.previousInput = null;
    this.operation = null;
    this.result = null;
    },
},
};
</script>

<style scoped>
/* Estilo principal */
.calculator-container {
max-width: 300px;
margin: 50px auto;
background: #333;
border-radius: 15px;
box-shadow: 0 10px 20px rgba(0, 0, 0, 0.5);
padding: 20px;
text-align: center;
color: white;
}

/* Display da calculadora */
.calculator-display {
background: #222;
color: #0f0;
font-size: 2rem;
padding: 20px;
margin-bottom: 20px;
border-radius: 10px;
text-align: right;
box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.5);
}

/* Botões */
.calculator-buttons {
display: grid;
grid-template-columns: repeat(4, 1fr);
gap: 10px;
}

.btn {
font-size: 1.2rem;
padding: 15px;
border: none;
border-radius: 10px;
cursor: pointer;
}

.btn-number {
background: #555;
color: white;
}

.btn-operation {
background: #f39c12;
color: white;
}

.btn-special {
background: #e74c3c;
color: white;
}

.btn-equals {
background: #27ae60;
color: white;
grid-column: span 4;
}

/* Interação */
.btn:active {
transform: scale(0.95);
box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.5);
}
</style>
