<template>
  <h1 class="text-center mt-3">VueJS - Calculator</h1>
  <div
    class="p-3"
    style="max-width: 400px; margin: 50px auto; background: #234"
  >
    <!-- Calculator result -->
    <div class="rounded m-1 lead p-2 font-weight-bold text-white bgdark">
      {{ cValue || 0 }}
    </div>

    <!-- Calculator button -->
    <div class="row">
      <div class="col-3" v-for="n in calculatorElements" :key="n">
        <div
          class="lead text-white text-center m-1 py-3 bgdark rounded hover-class"
          :class="{
            bggreen: ['C', '*', '/', '-', '+', '%', '='].includes(n),
          }"
          @click="action(n)"
        >
          {{ n }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TheCalculator",
  data: () => {
    return {
      cValue: "",
      calculatorElements: [
        "C",
        "*",
        "/",
        "-",
        7,
        8,
        9,
        "+",
        4,
        5,
        6,
        "%",
        1,
        2,
        3,
        "=",
        0,
        ".",
      ],
      operator: null,
      preCalcValue: "",
    };
  },

  methods: {
    action(n) {
      // Append value
      if (!isNaN(n) || n === ".") {
        this.cValue += n + "";
      }

      // Clear value
      if (n === "C") {
        this.cValue = "";
      }
      // Percentage
      if (n === "%") {
        this.cValue = this.cValue / 100 + "";
      }

      // Operators
      if (["/", "*", "-", "+"].includes(n)) {
        this.operator = n;
        this.preCalcValue = this.cValue;
        this.cValue = "";
      }

      // Calculate result using the eval function
      if (n === "=") {
        this.cValue = eval(this.preCalcValue + this.operator + this.cValue);
        this.preCalcValue = "";
        this.operator = null;
      }
    },
  },
};
</script>

<style scoped>
.bgdark {
  background: #2c88ea;
}
.hover-class:hover {
  cursor: pointer;
  background: #094382;
}
.bggreen {
  background: #10e387;
}
</style>
