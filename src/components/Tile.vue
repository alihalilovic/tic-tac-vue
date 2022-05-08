<script setup>
  defineProps(["tiles", "handleClick"])

  const emit = defineEmits(["tileClick"])
</script>

<template>
  <div
      class="tile"
      v-for="tile in tiles" :key="tile.position"
      @click="emit('tileClick', tile.position)"
      >
      {{ tile.sign }}
    </div>
</template>

<style scoped>
  .tile {
    border: 3px solid white;
    text-align: center;
    padding: 2.5rem;
    width: 2rem;
    height: 2rem;
    display: flex;
    font-weight: bold;
    border-radius: 20px;
    justify-content: center;
    align-items: center;
  }

  @media(max-width: 600px) {
    .tile {
      width: 1.5rem;
      height: 1.5rem;
    }
  }

  @media (max-width: 400px) {
    .tile {
      padding: 1.5rem;
    }
  }

  tile:nth-child(2) {
    background: blue;
  }

  .tile:hover {
    background: lightseagreen;
    cursor: pointer;
  }
</style>