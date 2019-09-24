<template>
  <v-container>
    <v-layout
      text-center
      wrap
    >
      <v-flex mb-4 py-10>
        <h1 class="display-2 font-weight-bold mb-3">
          Vue.js Calculator
        </h1>

        <v-card class="calculator">
          <CalculatorDisplay
            :result="result || 0">
            </CalculatorDisplay>

          <CalculatorButton
            :onClick="clear"
            class="operator clear">C
          </CalculatorButton>

          <CalculatorButton
            :onClick="percents"
            class="operator">%
          </CalculatorButton>

          <CalculatorButton
            :onClick="sum"
            class="operator">+
          </CalculatorButton>

          <CalculatorButton
            :onClick="appendNumber">1
          </CalculatorButton>

          <CalculatorButton
            :onClick="appendNumber">2
          </CalculatorButton>

          <CalculatorButton
            :onClick="appendNumber">3
          </CalculatorButton>

          <CalculatorButton
            :onClick="substract"
            class="operator">-
          </CalculatorButton>

          <CalculatorButton
            :onClick="appendNumber">4
          </CalculatorButton>

          <CalculatorButton
            :onClick="appendNumber">5
          </CalculatorButton>

          <CalculatorButton
            :onClick="appendNumber">6
          </CalculatorButton>

          <CalculatorButton
            :onClick="multiply"
            class="operator">*
          </CalculatorButton>

          <CalculatorButton
            :onClick="appendNumber">7
          </CalculatorButton>

          <CalculatorButton
            :onClick="appendNumber">8
          </CalculatorButton>

          <CalculatorButton
            :onClick="appendNumber">9
          </CalculatorButton>

          <CalculatorButton
            :onClick="divide"
            class="operator">/
          </CalculatorButton>

          <CalculatorButton
            :onClick="appendNumber"
            class="zero">0
          </CalculatorButton>

          <CalculatorButton
            :onClick="decimal">.
          </CalculatorButton>

          <CalculatorButton
            :onClick="equal"
            class="operator">=
          </CalculatorButton>

        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import CalculatorDisplay from './CalculatorDisplay'
import CalculatorButton from './CalculatorButton'

export default {
  name: 'Calculator',
  components: {
    CalculatorDisplay,
    CalculatorButton
  },
  data () {
    return {
      result: 0,
      previuousResult: null,
      operator: null,
      operatorClicked: false
    }
  },
  methods: {
    setPreviousResult () {
      this.previuousResult = this.result
      this.operatorClicked = true
    },
    
    clear () {
      this.result = ''
    },

    appendNumber (e) {
      if (this.operatorClicked) {
        this.result = ''
        this.operatorClicked = false
      }
      var value = e.target.innerText
      this.result = parseFloat(this.result + value)
    },

    percents () {
      this.result = this.result / 100
    },

    decimal () {
      this.result = this.result + ''
      if (this.result.indexOf('.') === -1) {
        this.result = this.result + '.'
      }
    },

    sum () {
      this.operator = (a,b) => a+b
      console.log(this.operator)
      this.setPreviousResult()
    },

    substract () {
      this.operator = (a,b) => b-a
      this.setPreviousResult()
    },

    multiply () {
      this.operator = (a,b) => a*b
      this.setPreviousResult()
    },

    divide () {
      this.operator = (a,b) => b/a
      this.setPreviousResult()
    },

    equal () {
      this.result = this.operator(
        parseFloat(this.result),
        parseFloat(this.previuousResult)
      )
      this.previuousResult = this.result
    },
  }
}
</script>

<style>
  .calculator {
    display: grid !important;
    grid-template-columns: repeat(4, 1fr);

    width: 350px;
    margin: 50px auto 0;

    border: 1px solid #000 !important
  }

  .calculator-display {
    grid-column: 1/5;
    padding: 10px 25px;
    font-size: 32px;
    text-align: right;

    border: 1px solid #000;
    background: #9e9e9e;
    color: #e5e5e5;
  }

  .calculator-button {
    border: 1px solid;
    border-radius: 0 !important;
    font-size: 22px !important;
    height: auto !important;
    padding-top: 15px !important;
    padding-bottom: 15px !important;
    background: #e5e5e5;
  }

  .clear {
    grid-column: 1/3;
  }

  .zero {
    grid-column: 1/3
  }

  .operator {
    background: orange;
  }
</style>
