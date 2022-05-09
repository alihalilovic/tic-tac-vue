<script setup>
  import { ref, watch } from "vue"
  import Tile from "./Tile.vue"
  import ResultBoard from "./ResultBoard.vue"

  const startingTiles = Array.from(Array(9).keys())
    .map(tile => {
      return { position: tile, sign: "" }
    })

  const tiles = ref([...startingTiles])

  const winningCombinations = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],

    [0, 4, 8],
    [1, 4, 7],
    [2, 4, 6],

    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8]
  ]
  
  const inputSign = ref("X")
  const winner = ref("")
  const gameFinished = ref(false)

  const gameRotation = () => {
    if (inputSign.value === "X") inputSign.value = "O"
    else inputSign.value = "X"
  }

  const handleTileClick = (position) => {
    if (gameFinished.value) return

    if (tiles.value[position].sign) {
      return
    }

    tiles.value[position].sign = inputSign.value
    gameRotation()
  }

  const checkIfWon = (temp, sign) => {
    if(temp[0] == sign && temp[1] == sign && temp[2] == sign) {
        gameFinished.value = true
        winner.value = sign
      }
  }

  const trackGameState = () => {
    const totalPlayedPositions = tiles.value.map(tile => tile.sign).filter(sign => sign)
    if (totalPlayedPositions.length == 9) {
      gameFinished.value = true
      winner.value = "DRAW"
    }

    winningCombinations.forEach(combination => {
      let temp = []

      combination.forEach(pos => {
        temp.push(tiles.value[pos].sign)
      })

      checkIfWon(temp, "X")
      checkIfWon(temp, "O")
    })
  }

  const restartGame = () => {
    gameFinished.value = false
    inputSign.value = "X"
    winner.value = ""

    tiles.value.map(tile => tile.sign = "")
  }

  watch(inputSign, () => {
    trackGameState()
  })
</script>

<template>
  <div class="container">
    <div class="board">
      <Tile
        :tiles="tiles"
        @tileClick="payload => handleTileClick(payload)" />
    </div>
    <Transition name="fade-result">
    <ResultBoard
      @restart="restartGame()"
      :gameFinished="gameFinished"
      :winner="winner" />
    </Transition>
  </div>
</template>

<style scoped>
  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: auto;
  }

  .board {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
  }

  .fade-result-enter-active,
  .fade-result-leave-active {
    transition: opacity 0.5s ease;
  }

  .fade-result-enter-from,
  .fade-result-leave-to {
    opacity: 0;
  }
</style>