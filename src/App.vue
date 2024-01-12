<template>
  <h3>Calculator</h3>
  <div class="in">
    <input type="number" @click="setOperandNumber(1)" v-model="input1">
    <p class="simbol">{{ simbol }}</p>
    <input type="number" @click="setOperandNumber(2)" v-model="input2">
  </div>
  <p class="result">{{ result }}</p>
  <div class="simbols">
    <button @click="simbol = '+'">+</button>
    <button @click="simbol = '-'">-</button>
    <button @click="simbol = '*'">*</button>
    <button @click="simbol = '/'">/</button>
    <button @click="simbol = 'x^n'">x^n</button>
    <button @click="simbol = '[x/n]'">[x/n]</button>
    <button @click="input1 = result; input2 = ''">inp1=res</button>
  </div>
  <div class="resultButtons">
    <button @click="functionResult(this.simbol)">=</button>
  </div>
  <div class="check">
    <input type="checkbox" @click="show = !show" />
  </div>
  <div v-show="show" class="keyboard">
    <button v-for="item of buttons" @click="setNumeral(item, operandNumber)">{{ item }}</button>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {

  },
  data() {
    return {
      operandNumber: 1,
      simbol: "",
      input1: '',
      input2: "",
      result: 0,
      show: '',
      buttons: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, '<-']
    }
  },
  methods: {
    setNumeral(item, operandNumber) {
      if (operandNumber == 1 && typeof (item) === "number") {
        this.input1 = `${this.input1}${item}`;
      } else if (operandNumber == 1 && item === '<-') {
        this.input1 = this.input1.slice(0, this.input1.length - 1);
      }
      if (operandNumber == 2 && typeof (item) === "number") {
        this.input2 = `${this.input2}${item}`;
      } else if (operandNumber == 2 && item === '<-') {
        this.input2 = this.input2.slice(0, this.input2.length - 1);
      }
    },
    setOperandNumber(number) {
      this.operandNumber = number;
    },
    functionResult(simbol) {

      if (simbol === "+") {
        this.result = Number(this.input1) + Number(this.input2);
      }
      if (simbol === "-") {
        this.result = Number(this.input1) - Number(this.input2);
      }
      if (simbol === "*") {
        this.result = Number(this.input1) * Number(this.input2);
      }
      if (simbol === "/" && this.input2 == 0) {
        this.result = "делить на ноль нельзя"
      }
      if (simbol === "/" && !this.input2 == 0) {
        this.result = Number(this.input1) / Number(this.input2);
      }
      if (simbol === "x^n") {
        this.result = Math.pow(Number(this.input1), Number(this.input2));
      }
      if (simbol === "[x/n]") {
        this.result = parseInt(Number(this.input1) / Number(this.input2))
      }
      return this.result;
    }
  }

}
</script>

<style lang="scss">
.txtprop {
  color: rgb(56, 126, 28);
  text-shadow: #2c3e50;
  font-weight: 800;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 30px;
  border: 1px solid black;
  max-width: max-content;
  margin: 50px auto;
  gap: 5px;
  padding: 5px;
}

p {
  min-height: 24px;
  margin: 0 auto;
  @extend.txtprop;
}

.simbols button {
  margin: 2px;
  padding: 2px 5px;
}

.resultButtons {
  width: 100%;

  button {
    box-sizing: border-box;
    width: inherit;
    padding: 2px 5px;
  }
}

.keyboard {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 3px;
}
</style>
