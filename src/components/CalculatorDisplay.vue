<template>
    <div class="calculator-display">
        {{result}}
    </div>
</template>

<script>

export default {
  name: 'CalculatorDisplay',
  props: {
    result: {
      type: Number,
      required: true
    }
  }
}
</script>
