<template>
  <v-card>
    <v-container>
      <v-row justify="center">
        <code v-if="num1 || num2 || op">{{num1}} {{op}} {{num2}} {{result ? ` = ${result}`:""}}</code>
        <code v-else>Start typing something</code>
      </v-row>
    </v-container>
  </v-card>
</template>
<script>
export default {
  name: "Result",
  props: ["num1", "num2", "op", "result"]
};
</script>
