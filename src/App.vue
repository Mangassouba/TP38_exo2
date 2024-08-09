<!-- src/App.vue -->
<template>
  <div id="app">
    <h1>Formulaire</h1>
    <formulaireComponents />
  </div>
</template>

<script setup>
import formulaireComponents from './components/formulaireComponents.vue';
</script>

<style>
/* Styles globaux */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
