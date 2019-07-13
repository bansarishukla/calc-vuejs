<template>
  <div class="outerBox">
    <div class = "calculator">
      <div class="display">{{ current || '0'}}</div>
      <div v-for="number in numbers" class="btn">
        <cal-button :val="number" @append="append"></cal-button>
      </div>
      <div class="btn" @click="add">+</div>
      <div class="btn" @click="dot">.</div>
      <div class="btn" @click="percentage">%</div>
      <div class="btn" @click="divide">÷</div>
      <div class="btn" @click="mul">×</div>
      <div class="btn" @click="sub">-</div>
      <div class="btn equalto" @click="equal">=</div>
      <div class="btn" @click="clear">C</div>
      <div class="btn" @click="back"><</div>

    </div>
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
        displayValue : "",
        previous: null,
        operator: null,
        operatorClick: false,
        ansValue : null,
        numbers: [9,8,7,6,5,4,3,2,1,0]
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
        parseFloat(this.previous),
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
    border: 1px solid dimgray;
    border-radius: 4px;
  }
  .display {
    grid-column: 1 / 5;
    display:block;
    background-color: gainsboro;
    padding:20px;
    height:100px;
    border-radius:10px;
    text-align: end;
    font-weight: bold;
  }
  .btn {
    border: 1px solid white;
    font-weight: bold;
    padding:  0 0 0 0;
    padding: 15px;
  }
  .btn:hover {
    background-color: black;
    color: white;
    font-weight: bold;
  }
  .equalto {
    grid-column: 1 / 3;

  }
</style>
