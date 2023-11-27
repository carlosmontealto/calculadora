<template>
  <div class="container">
    <form>
      <div class="labelBlock">
        <label class="label" for="number1">
          Numero 1
        </label>
        <input class="textCamp" @change="calculate(operation)" v-model="number1" type="number" id="number1" />
      </div>
      <div class="labelBlock">
        <label class="label" for="number2">
          Numero 2
        </label>
        <input class="textCamp" @change="calculate(operation)" v-model="number2" type="number" id="number2" />
      </div>
      <div class="labelBlock">
        <label class="label" for="operation">
          Operação
        </label>
        <select class="textCamp" @change="calculate(operation)" v-model="operation" id="operation">
          <option value="sum">Soma</option>
          <option value="subtract">Subtração</option>
          <option value="multiply">Multiplicação</option>
          <option value="divide">Divisão</option>
        </select>
      </div>      
    </form>
    <p v-if="isValid === true" class="p">Resultado da conta: </p>
    <span id="result">{{ result }}</span>
  </div>
</template>

<script>



export default {
  data() {
    return {
      number1: "",
      number2: "",
      operation: "",
      result: "",
      isValid: true
    };
  },
  methods: {
    calculate(operation) {
      const num1 = parseFloat(this.number1);
      const num2 = parseFloat(this.number2);

      if (isNaN(num1) || isNaN(num2)) {
        this.isValid = false;
        this.result = 'Apresente dois números validos e selecione uma operação matemática';
        return;
      }

      switch (operation) {
        case "sum":
          this.result = num1 + num2;
          this.isValid = true;
          break;
        case "subtract":
          this.result = num1 - num2;
          this.isValid = true;
          break;
        case "multiply":
          this.result = num1 * num2;
          this.isValid = true;
          break;
        case "divide":
          if (num2 === 0) {
            this.isValid = false;
            this.result = "Divisão por zero não é possível";
            return;
          }
          this.isValid = true;
          this.result = num1 / num2;
          break;
        default:
          this.isValid = false;
      }
    }
  }
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
  box-sizing: border-box;
  display: block;
}

.container {
  max-width: 960px;
  margin: 0 auto;
}

.labelBlock {
  display: flex;
  margin-bottom: 8px;
}

.label {
  margin-right: 8px;
}

.p {
  display: flex;
}

.textCamp {
  padding: 4px;
  border-radius: 8px;
}

</style>
