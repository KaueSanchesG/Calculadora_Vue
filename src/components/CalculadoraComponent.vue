<template>
<div class="hello">
    <h1>{{ msg }}</h1>

<table class="table table-bordered">
      <tbody>
        <tr>
          <td colspan="4">{{output || 0}}</td>
        </tr>
        <tr>
          <td @click="clearField">C</td>
          <td>+/-</td>
          <td @click="calculatePercent">%</td>
          <td class="right-column">/</td>
        </tr>
        <tr>
          <td>7</td>
          <td>8</td>
          <td>9</td>
          <td class="right-column">x</td>
        </tr>
        <tr>
          <td>4</td>
          <td>5</td>
          <td>6</td>
          <td class="right-column">-</td>
        </tr>
        <tr>
          <td>1</td>
          <td>2</td>
          <td>3</td>
          <td class="right-column">+</td>
        </tr>
        <tr>
          <td colspan="2">0</td>
          <td>.</td>
          <td class="right-column">=</td>
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
  data(){
    return{
      output:'12'
    }
  },
  methods:{
  clearField(){
    this.output ='0'
   },
  calculatePercent(){
      this.output /= 100;
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

tr{
  background-image: linear-gradient(-80deg, #BFF098, #6FD6FF);
}
.right-column{
  /* background-color: darkcyan; */
  /*background-image: linear-gradient(-80deg, #C6EA8D, #FE90AF);*/
  /* border-radius: 7px; */
  color: blue;
}
td:active{
  background-image: none;
  background-color: lightgray;
}
</style>
