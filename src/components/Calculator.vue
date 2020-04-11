<template>
  <div class="calculator">
    <div class="display" id="numberdisp">{{ current || '0'}}</div>
    <div @click="clear" class="btn pointer">C</div>
    <div @click="sign" class="btn pointer">+/-</div>
    <div @click="pcent" class="btn pointer">%</div>

    <div @click="divide()" class="btn operator pointer">÷</div>

    <div @click="addDigit('7')" class="btn pointer">7</div>
    <div @click="addDigit('8')" class="btn pointer">8</div>
    <div @click="addDigit('9')" class="btn pointer">9</div>

    <div @click="multiply()" class="btn operator pointer">x</div>

    <div @click="addDigit('4')" class="btn pointer">4</div>
    <div @click="addDigit('5')" class="btn pointer">5</div>
    <div @click="addDigit('6')" class="btn pointer">6</div>

    <div @click="substract()" class="btn operator pointer">-</div>

    <div @click="addDigit('1')" class="btn pointer">1</div>
    <div @click="addDigit('2')" class="btn pointer">2</div>
    <div @click="addDigit('3')" class="btn pointer">3</div>

    <div @click="sum()" class="btn operator pointer">+</div>

    <div @click="addDigit('0')" class="btn zero pointer">0</div>
    <div @click="comma()" class="btn pointer">.</div>

    <div @click="equal()" class="btn operator pointer" id="equal">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: '168465155',
      clicked: false,
      previous: null,
      operator: null,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },

    sign() {
      this.current = ((-1)*parseInt(this.current, 10)).toString();
    },

    pcent() {
      this.current = parseFloat(this.current) / 100
    },

    addDigit(number) {
      if (this.clicked) {
        this.current = '';
        this.clicked = false;
      }
      this.current += number;
    },

    comma() {
      if (this.current.indexOf('.') == -1) {
        this.addDigit('.');
      }
    },

    setPrevious() {
      this.previous = this.current;
      this.clicked = true;
    },

    sum() {
      this.operator = '+'
      this.setPrevious();
    },

    multiply() {
      this.operator = 'x';
      this.setPrevious();
    },

    divide() {
      this.operator = '/';
      this.setPrevious();
    },

    substract() {
      this.operator = '-';
      this.setPrevious();
    },

    operate(operator) {
      switch (operator) {
        case '+': this.current = 
        parseFloat(this.current, 10) +
        parseFloat(this.previous, 10);
        break;

        case '-':this.current = 
        parseFloat(this.previous, 10)
        - parseFloat(this.current, 10);
        break;

        case 'x':this.current = 
        parseFloat(this.current, 10) *
        parseFloat(this.previous, 10);
        break;

        case '/':this.current = 
        parseFloat(this.previous, 10) /
        parseFloat(this.current, 10);
        break;

        default: this.current = 0
        break;
      }
    },

    equal() {
      if (this.previous != null) {
        this.operate(this.operator);
        this.previous = null;
      }
      
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.calculator {
  border: solid 2px black;
  margin: 0 auto;
  width: 350px;
  font-size: 30px;
  display: grid;
  grid-template-columns: repeat(4, auto);
  grid-auto-rows: minmax(0px, auto);
  font-family: Arial;
  border-radius: 15px 15px 15px 15px;
}

.display {
  padding-right: 10px;
  overflow: hidden;
  direction: rtl;
  grid-column: 1 / 5;
  background-color: #eeeeee;
  color: black;
  height: 100px;
  text-align: right;
  border: 1px solid #e0e0e0;
}

.zero {
  border: 1px solid #e0e0e0;
  grid-column: 1 / 3;
}

.btn {
  background-color: white;
  border: 1px solid #e0e0e0;
  padding-left: 5px;
  padding-right: 5px;
  padding-top: 5px;
  padding-bottom: 5px;
}

.btn:hover {
  background: rgb(204, 203, 203);
}

.btn:active {
  background: #e0e0e0;
}

.operator {
  border: 1px solid #e0e0e0;
  background-color: #4db2ec;
  color: white;
}

.operator:hover {
  background-color: #1fa1ec;
}

.operator:active {
  background-color: #4db2ec;
}

.pointer {
  cursor: pointer;
}


</style>
