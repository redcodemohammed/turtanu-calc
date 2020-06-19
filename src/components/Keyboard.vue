<template>
  <v-container>
    <v-card elevation="10" :loading="loading" class="pa-4">
      <v-container>
        <v-row class="justify-space-between">
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeNumber('7')">7</v-btn>
          </v-col>
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeNumber('8')">8</v-btn>
          </v-col>
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeNumber('9')">9</v-btn>
          </v-col>
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="delNumber">
              <v-icon>mdi-backspace</v-icon>
            </v-btn>
          </v-col>
        </v-row>
        <v-row class="justify-space-between">
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeNumber('4')">4</v-btn>
          </v-col>
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeNumber('5')">5</v-btn>
          </v-col>
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeNumber('6')">6</v-btn>
          </v-col>
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeOp('×')">×</v-btn>
          </v-col>
        </v-row>
        <v-row class="justify-space-between">
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeNumber('1')">1</v-btn>
          </v-col>
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeNumber('2')">2</v-btn>
          </v-col>
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeNumber('3')">3</v-btn>
          </v-col>
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeOp('÷')">÷</v-btn>
          </v-col>
        </v-row>
        <v-row class="justify-space-between">
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeNumber('0')">0</v-btn>
          </v-col>
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeOp('+')">+</v-btn>
          </v-col>
          <v-col cols="3">
            <v-btn block :disabled="loading" @click="changeOp('-')">-</v-btn>
          </v-col>
          <v-col cols="3">
            <v-btn block :disabled="loading || !valid" @click="calc">=</v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-card>
  </v-container>
</template>
<script>
export default {
  name: "Keyboard",
  props: ["loading", "valid"],
  methods: {
    changeOp(op) {
      this.$emit("changeOp", op);
    },
    changeNumber(n) {
      this.$emit("changeNumber", n);
    },
    delNumber() {
      this.$emit("delNumber");
    },
    calc() {
      this.$emit("calc");
    }
  }
};
</script>
