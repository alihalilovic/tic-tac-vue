<script setup>
  import { ref } from "vue"

  import Game from './components/Game.vue';


</script>

<template>
  <h1>Tic Tac Toe</h1>
  <Game />
</template>

<style>
  #app {
    font-family: "Nunito";
    font-size: 1.5rem;
    color: white;
  }

  h1 {
    text-align: center;
    text-transform: uppercase;
    font-weight: 200;
  }

  body {
    background: #111;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
