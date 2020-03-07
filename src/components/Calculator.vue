<template>
  <div class="body">
    <div class="screen">{{ screen || 0 }}</div>
    <div @click="append('7')" class="item">7</div>
    <div @click="append('8')" class="item">8</div>
    <div @click="append('9')" class="item">9</div>
    <div @click="setOp('/')" class="item operator right">/</div>
    <div @click="back" class="item right">BACK</div>
    <div @click="append('4')" class="item">4</div>
    <div @click="append('5')" class="item">5</div>
    <div @click="append('6')" class="item">6</div>
    <div @click="setOp('*')" class="item operator right">x</div>
    <div @click="clear" class="item right">AC</div>
    <div @click="append('1')" class="item">1</div>
    <div @click="append('2')" class="item">2</div>
    <div @click="append('3')" class="item">3</div>
    <div @click="setOp('-')" class="item operator right">-</div>
    <div class="item"></div>
    <div @click="append('0')" class="item">0</div>
    <div @click="dot" class="item">.</div>
    <div class="item"></div>
    <div @click="setOp('+')" class="item operator right">+</div>
    <div @click="calculate" class="item right">=</div>    
  </div>
</template>

<script>
export default {
  data() {
    return {
      leftNum: '',
      operator: '',
      rightNum: '',
      screen: ''
    }
  },
  methods: {
    append(number) {
      if (this.rightNum === '' && this.operator === '') {
        this.leftNum = `${this.leftNum}${number}`
        this.screen = this.leftNum;
      }
      else {
        this.rightNum = `${this.rightNum}${number}`;
        this.screen = this.rightNum;
      }
    },
    setOp(op) {
      this.operator = op;
      this.calculate();
    },
    dot() {
      if (this.operator === '') {
        if (this.leftNum.indexOf('.') === -1) {
          this.leftNum = `${this.leftNum}.`;
          this.screen = this.leftNum;
        }
      }
      else {
        if (this.rightNum.indexOf('.') === -1) {
          this.rightNum = `${this.rightNum}.`;
          this.screen = this.rightNum;
        }
      }
    },
    clear() {
      this.screen = '';
      this.leftNum = '';
      this.rightNum = '';
      this.operator = '';
    },
    back() {
      if(this.leftNum != '' && this.rightNum === '' && this.operator === '') {
        this.leftNum = this.leftNum.slice(0, -1);
        this.screen = this.leftNum;
      }
      else if (this.rightNum != '') {
        this.rightNum = this.rightNum.slice(0, -1);
        this.screen = this.rightNum;
      }
    },
    add(a, b) {
      return (parseFloat(a) + parseFloat(b)).toString();
    },
    sub(a, b) {
      return (parseFloat(a) - parseFloat(b)).toString();
    },
    mult(a, b) {
      return (parseFloat(a) * parseFloat(b)).toString();
    },
    div(a, b) {
      if (b === '0')
        return 'Undefined';
      return (parseFloat(a) / parseFloat(b)).toString();
    },
    operate(op, a, b) {
      switch(op) {
        case '+':
          return this.add(a, b);
        case '-':
          return this.sub(a, b);
        case '*':
          return this.mult(a, b);
        case '/':
          return this.div(a, b);
      }
    },
    calculate() {
      if (this.leftNum != '' && this.operator != '' && this.rightNum != '')
      {
        this.screen = this.operate(this.operator, this.leftNum, this.rightNum);
        this.leftNum = this.screen;
        this.rightNum = '';
      }
    }
  }
}
</script>

<style scoped>
.body {
  display: grid;
  margin: 0 auto;
  width: 450px;
  font-size: 40px;
  grid-template-columns: repeat(5, 1fr);
  grid-auto-rows: minmax(100px, auto);
  background-color: black;
}

.screen {
  text-align: end;
  grid-column: 1 / 6;
  background-color: rgb(44,44,44);
  border-bottom: 1px solid gray;
  color: white;
  font-size: 45px;
  padding-top: 35px;
  padding-right: 20px;
}

.item {
  background-color: rgb(44,44,44);
  color: white;
  border: none;
  padding-top: 40px;
  font-size: 25px;
}

.item:hover { background-color: rgb(55, 55,55) }

.item:focus { outline: 0 }

.operator { border-left: 1px solid gray; }

.right { color: lightblue; }
</style>