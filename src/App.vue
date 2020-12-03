<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <formata-valor valor="12" />
</template>

<script>
import FormataValor from "@/components/FormataValor.vue";

export default {
  name: "App",
  components: {
    FormataValor,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
