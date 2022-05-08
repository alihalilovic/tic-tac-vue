<script setup>
  defineProps(["gameFinished", "winner"])

  const emit = defineEmits(["restart"])

</script>

<template>
  <div class="result" v-if="gameFinished">
    <p v-if="winner == 'DRAW'">It's a draw!</p>
    <p v-else>
      Player {{ winner }} won!
    </p>
    <button @click="emit('restart')">Restart game</button>
    <footer>
    made with 🤍 by <a href="https://github.com/alihalilovic">@alihalilovic</a>
    </footer>
  </div>
  
</template>

<style scoped>
  .result {
    text-transform: uppercase;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .result p {
    font-size: 2rem;
  }

  button {
    border: none;
    outline: none;
    padding: 1.2rem 2rem;
    text-transform: uppercase;
    color: white;
    font-weight: 200;
    font-size: 1.1rem;
    background: lightseagreen;
    letter-spacing: .5rem;
    transition: 0.2s ease;
  }

  button:hover {
    background: white;
    color: lightseagreen;
  }

  footer {
    margin-top: 2rem;
    font-size: 1.1rem;
    text-transform: none;
    opacity: 0.4;
  }

  a {
    color: white;
  }
</style>