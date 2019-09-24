<template>
    <v-btn text class="calculator-button" @click="onClick">
        <slot>Button</slot>
      </v-btn>
</template>

<script>

export default {
  name: 'CalculatorButton',

  props: {
    onClick: {
      type: Function,
      required: true
    }
  }
}
</script>
