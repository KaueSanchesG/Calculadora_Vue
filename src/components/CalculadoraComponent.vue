<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <table class="table table-bordered">
      <tbody>
        <tr>
          <td colspan="4">{{ output || 0 }}</td>
        </tr>
        <tr>
          <td @click="clearField">C</td>
          <td @click="setNegativelOrPositive">+/-</td>
          <td @click="processOutput('percent')">%</td>
          <td @click="processOutput('divide')" class="right-column">/</td>
        </tr>
        <tr>
          <td @click="getNumber('7')">7</td>
          <td @click="getNumber('8')">8</td>
          <td @click="getNumber('9')">9</td>
          <td @click="processOutput('multiply')" class="right-column">x</td>
        </tr>
        <tr>
          <td @click="getNumber('4')">4</td>
          <td @click="getNumber('5')">5</td>
          <td @click="getNumber('6')">6</td>
          <td @click="processOutput('substract')" class="right-column">-</td>
        </tr>
        <tr>
          <td @click="getNumber('1')">1</td>
          <td @click="getNumber('2')">2</td>
          <td @click="getNumber('3')">3</td>
          <td @click="processOutput('plus')" class="right-column">+</td>
        </tr>
        <tr>
          <td @click="getNumber('0')" colspan="2">0</td>
          <td @click="getDot()">.</td>
          <td @click="updateOutput" class="right-column">=</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

export default {
  name: 'CalculadoraComponent',
  props: {
    msg: String
  },
  data() {
    return {
      output: '',
      previousValue: null,
      operationFired: false
    }
  },
  methods: {
    clearField() {
      this.output = ''
    },
    setNegativelOrPositive() {
      this.output = this.output[0] === '-' ? this.output.slice(1) : `-${this.output}`
    },
    getNumber(number) {
      if (this.operationFired) {
        this.output = '';
        this.operationFired = false;
      }
      this.output = `${this.output}${number}`
    },
    getDot() {
      if (this.output.indexOf('.') === -1) {
        this.output += '.';
      }
    },
    processOutput(op) {
      switch (op) {
        case 'plus':
          this.op = (a, b) => {
            return parseFloat(a) + parseFloat(b);
          }
          break;
        case 'substract':
          this.op = (a, b) => {
            return parseFloat(a) - parseFloat(b);
          }
          break;
        case 'divide':
          this.op = (a, b) => {
            return parseFloat(a) / parseFloat(b);
          }
          break;
        case 'multiply':
          this.op = (a, b) => {
            return parseFloat(a) * parseFloat(b);
          }
          break;
        case 'percent':
          this.op = (a, b) => {
            if (a != null && b != null) {
              return (parseFloat(a) * parseFloat(b)) / 100;
            } else {
              return parseFloat(b) / 100;
            }
          }
          break;
      }
      this.previousValue = this.output;
      this.operationFired = true;
    },
    updateOutput() {
      this.output = `${this.op(this.previousValue, this.output)}`;
      this.previousValue = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

tr {
  background-image: linear-gradient(-80deg, #BFF098, #6FD6FF);
}

.right-column {
  /* background-color: darkcyan; */
  /*background-image: linear-gradient(-80deg, #C6EA8D, #FE90AF);*/
  /* border-radius: 7px; */
  color: blue;
}

td:active {
  background-image: none;
  background-color: lightgray;
}
</style>
