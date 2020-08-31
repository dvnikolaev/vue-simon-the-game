<template>
  <div class="options">
    <div class="options-difficulty">
      <h3 class="options-difficulty__header">Сложность:</h3>
      <label>
        <input type="radio" name="difficult" checked>
        <span>Легко</span>
      </label>
      <label>
        <input type="radio" name="difficult">
        <span>Нормально</span>
      </label>
      <label>
        <input type="radio" name="difficult">
        <span>Сложно</span>
      </label>
    </div>
    <button class="options__button" @click="startGame" :disabled="isStart">старт</button>
  </div>
</template>

<script>
export default {
  props: {
    isStart: Boolean
  },
  methods: {
    startGame() {
      this.$emit('startGame');
    }
  }
}
</script>

<style>
  .options {
    margin-left: 100px;
    background-color: white;
    padding: 25px;
    border-radius: 10px;
  }
  .options-difficulty__header {
    margin: 10px 0;
  }
  .options__button {
    width: 100%;
    padding: 10px;
    margin-top: 30px;
    font-size: 16px;
    font-weight: bold;
    text-transform: uppercase;
    color: white;
    background-color: #00c6ff;
    border: none;
    letter-spacing: 2px;
    cursor: pointer;
  }
  .options__button:disabled {
    background-color: rgb(190, 190, 190);
  }
</style>