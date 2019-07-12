<template>
  <div class = "calculator">
    <div class="display">{{ current || '0'}}</div>
    <!-- <div class="btn" @click="clear">C</div>
    <div class="btn" @click="back"><</div>
    <div class="btn" @click="percentage">%</div>
    <div class="btn" @click="divide">÷</div>
    <div class="btn" @click="append(9)">9</div>
    <div class="btn" @click="append(8)">8</div>
    <div class="btn" @click="append(7)">7</div>
    <div class="btn" @click="mul">×</div>
    <div class="btn" @click="append(4)">4</div>
    <div class="btn" @click="append(5)">5</div>
    <div class="btn" @click="append(6)">6</div>
    <div class="btn" @click="sub">-</div>
    <div class="btn" @click="append(1)">1</div>
    <div class="btn" @click="append(2)">2</div>
    <div class="btn" @click="append(3)">3</div>
    <div class="btn" @click="add">+</div>
    <div class="btn zero" @click="append(0)">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn" @click="equal">=</div> -->
    <cal-button val="1" @append="append"></cal-button>
    <cal-button val="2" @append="append"></cal-button>
    <cal-button val="4" @append="append"></cal-button>
    <cal-button val="5" @append="append"></cal-button>
    <cal-button val="6" @append="append"></cal-button>
    <cal-button val="7" @append="append"></cal-button>
    <cal-button val="8" @append="append"></cal-button>
    <cal-button val="9" @append="append"></cal-button>
    <cal-button val="0" @append="append"></cal-button>

    <!-- <div class="btn" @click="back"><</div> -->
  </div>
</template>

<script>
import CalButton from './CalButton'
export default {
  components: {
    'cal-button': CalButton
  },
  data() {
    return {
        current: '',
        previous: null,
        operator: null,
        operatorClick: false
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    percentage() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    back() {
      const arr = this.current.split('')
      arr.pop()
      this.current = arr.join('')
    },
    append(number) {
      if(this.operatorClick){
        this.current = '';
        this.operatorClick = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot(){
      if(this.current.indexOf('.') === -1){
        this.append('.');
      }
    },
    divide() {
      this.operator = (a,b) => b/a;
      this.setPrev();
    },
    mul() {
      this.operator = (a,b) => a*b;
      this.setPrev();
    },
    sub() {
      this.operator = (a,b) => b-a;
      this.setPrev();
    },
    add() {
      this.operator = (a,b) => a+b;
      this.setPrev();
    },
    equal() {
      this.current = this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      );
      this.previous = null;
    },
    setPrev() {
      this.previous = this.current;
      this.operatorClick = true;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator {
    width: 20%;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4 , 1fr);
    grid-auto-rows: minmax(50px, auto);
    background-color: pink;
  }
  .display {
    grid-column: 1 / 5;
    background:lightgrey;
    color: white;
    padding: 15px;
    text-align: end;
  }
  .btn {
    border: 5px solid white;
    padding: 10px;
    font-weight: bold;
  }
  .zero {
    grid-column: 1 / 3;
  }
</style>
