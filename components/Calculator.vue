<template>
  <div class="content">
    <h1>{{ (num2 ? num2 : num1) || "0" }}</h1>
    <div class="style-button">
      <button @click="clear()" class="sinals">AC</button>
      <button class="sinals">+/-</button>
      <button @click="percent()" class="sinals">%</button>
      <button @click="divide()" class="sinals">/</button>
      <button @click="append('7')">7</button>
      <button @click="append('8')">8</button>
      <button @click="append('9')">9</button>
      <button @click="multiple()" class="sinals">x</button>
      <button @click="append('4')">4</button>
      <button @click="append('5')">5</button>
      <button @click="append('6')">6</button>
      <button @click="minus()" class="sinals">-</button>
      <button @click="append('1')">1</button>
      <button @click="append('2')">2</button>
      <button @click="append('3')">3</button>
      <button @click="plus()" class="sinals">+</button>
      <button @click="append('0')">0</button>
      <button @click="dot()" class="sinals">.</button>
      <button @click="equal()" class="equal">=</button>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class Calculator extends Vue {
  public num1 = "1";
  public num2 = "";
  public operator: (a: number, b: number) => string = () => "";
  public operatorClicked = false;

  public clear() {
    this.num1 = "";
    this.num2 = "";
    this.operatorClicked = false;
  }

  public equal() {
    this.num1 = `${this.operator(Number(this.num1), Number(this.num2))}`;
    this.num2 = "";
  }

  public plus() {
    if (this.num2) this.equal();
    this.operator = (a, b) => String(a + b);
    this.operatorClicked = true;
  }

  public minus() {
    if (this.num2) this.equal();
    this.operator = (a, b) => String(a - b);
    this.operatorClicked = true;
  }

  public divide() {
    if (this.num2) this.equal();
    this.operator = (a, b) => String(a / b);
    this.operatorClicked = true;
  }

  public multiple() {
    if (this.num2) this.equal();
    this.operator = (a, b) => String(a * b);
    this.operatorClicked = true;
  }

  public percent() {
    if (this.num2) this.equal();
    this.operator = (a) => String(a / 100);
    this.operatorClicked = true;
  }

  public dot() {
    this.append2(".");
  }

  public append2(num: string) {
    if (this.operatorClicked) {
      this.num2 = `${this.num2}${num}`;
    } else {
      this.num1 = `${this.num1}${num}`;
    }
  }

  public append(num: number) {
    if (this.operatorClicked) {
      this.num2 = `${this.num2}${num}`;
    } else {
      this.num1 = `${this.num1}${num}`;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
button {
  width: 70px;
  height: 70px;
  cursor: pointer;
  border-radius: 100%;
  border-color: black;
  font-size: 20px;
}

.style-button {
  padding: 30px;
  margin-left: -30px;
  margin-right: 20px;
  width: 100%;
  height: 360px;
  margin-top: 30px;
}

.content {
  background-color: black;
  width: 300px;
  height: 500px;
  align-items: center;
  flex-direction: column;
  padding: 15px;
  border-radius: 20px;
  margin-left: 300px;
}

.sinals {
  background-color: #ccff33;
}

.equal {
  width: 140px;
  height: 60px;
  border-radius: 12px;
  font-size: 30px;
}

.content h1 {
  color: black;
  justify-content: right;
  display: flex;
  background-color: white;
  margin-top: 120px;
  padding: 16px;
  margin: auto;
  border-radius: 100px;
}

h1 {
  margin-top: -15px;
}
</style>