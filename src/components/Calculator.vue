<template>
  <div class="calculator">
    <div class="display">{{ current || '0' }}</div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="divide()">/</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="times()">X</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="minus()">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="add()">+</div>
    <div class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="dot()">.</div>
    <div class="btn operator" @click="equal()">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "0",
      operator: null,
      previuos: null,
      previuosCliced: false
    };
  },
  methods: {
    clear: function() {
      this.current = "";
    },

    sign: function() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },

    percent: function() {
      this.current = `${parseFloat(this.current / 100)}`;
    },

    append: function(num) {
      if(this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${num}`;
    },

    dot: function() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },

    divide: function() {
      this.operator = (a, b) => a / b;
      this.setPreviuos();
    },

    times: function() {
      this.operator = (a, b) => a * b;
      this.setPreviuos();
    },

    minus: function() {
      this.operator = (a, b) => a - b;
      this.setPreviuos();
    },

    add: function() {
      this.operator = (a, b) => a + b;
      this.setPreviuos();
    },

    setPreviuos: function() {
      this.previuos = this.current;
      this.operatorClicked = true;
    },

    equal: function() {
      this.current = `${this.operator(parseFloat(this.current), parseFloat(this.previuos))}`;
      this.previuos = null;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 40px;
  width: 500px;
  margin: 0 auto;
}

.display {
  grid-column: 1 / 5;
  background: #333;
  color: #fff;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  background: #f2f2f2;
  border: 1px solid #333;
}

.operator {
  background: orange;
  color: #fff;
}
</style>
