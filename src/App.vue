<template>
  <v-app>
    <nav>
      <AppBar />
    </nav>
    <v-main>
      <v-container>
        <v-row class="justify-center">
          <v-col cols="10" xl="5" md="5" sm="10" xs="10">
            <Result :loading="loading" :num1="num1" :num2="num2" :op="op" :result="result" />
          </v-col>
        </v-row>
        <v-row class="justify-center">
          <v-col cols="12" xl="6" md="6" sm="12" xs="12">
            <Keyboard
              @changeOp="changeOp"
              @changeNumber="changeNumber"
              @delNumber="delNumber"
              @calc="calc"
              :loading="loading"
              :valid="valid"
            />
          </v-col>
        </v-row>
      </v-container>
      <v-snackbar v-model="error">
        Please check your internet connection
        <v-btn text color="error" @click.native="error = false">Close</v-btn>
      </v-snackbar>
    </v-main>
  </v-app>
</template>

<script>
import Keyboard from "./components/Keyboard";
import Result from "./components/Result";
import AppBar from "./components/layout/AppBar";

export default {
  name: "App",

  components: {
    Keyboard,
    AppBar,
    Result
  },

  data: () => ({
    num1: "",
    num2: "",
    op: "",

    result: "",

    loading: false,
    error: false,

    memory: {}
  }),

  computed: {
    valid() {
      return this.num1 !== "" && this.num2 !== "";
    }
  },

  methods: {
    changeOp(val) {
      this.op = val;
    },
    changeNumber(val) {
      this.result = "";
      if (this.op === "") {
        if (this.num1 === "" && val === "0") return;
        else this.num1 = this.num1.concat(val);
      } else {
        if (this.num2 === "" && val === "0") return;
        else this.num2 = this.num2.concat(val);
      }
    },
    delNumber() {
      this.result = "";
      if (this.num2.length > 0)
        this.num2 = this.num2.substring(0, this.num2.length - 1);
      else if (this.op !== "") this.op = "";
      else this.num1 = this.num1.substring(0, this.num1.length - 1);
    },
    async calc() {
      let { num1, op, num2 } = this;
      switch (op) {
        case "+":
          op = "sum";
          break;
        case "-":
          op = "sub";
          break;
        case "×":
          op = "mul";
          break;
        case "÷":
          op = "div";
          break;
      }
      if (this.memory[`${num1} ${op} ${num2}`]) {
        this.result = this.memory[`${num1} ${op} ${num2}`];
      } else {
        this.loading = true;
        try {
          let resultRes = await fetch(
            `https://tur-calculator.herokuapp.com/?num1=${num1}&num2=${num2}&op=${op}`
          );
          let result = await resultRes.json();
          this.result = result.result;
          this.memory[`${num1} ${op} ${num2}`] = this.result;
          this.loading = false;
        } catch {
          this.loading = false;
          this.error = true;
        }
      }
    }
  }
};
</script>
