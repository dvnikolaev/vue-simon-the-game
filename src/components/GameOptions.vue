<template>
  <div class="options">
    <div class="options-difficulty">
      <h3 class="options-difficulty__header">Сложность:</h3>
      <label v-for="item in difficultyArray" :key="item.value">
        <input
          type="radio"
          name="difficulty"
          :value="item.value"
          @change="updateDiffuclty(item.value)"
          :checked="item.value === difficulty"
          :disabled="isStart"
        />
        <span>{{ item.text }}</span>
      </label>
    </div>
    <button class="options__button" @click="startGame" :disabled="isStart">
      старт
    </button>
    <div class="difficulty-description">
      <p>Легко - Время между каждой кнопкой - 1.5с.</p>
      <p>Нормально - Время между каждой кнопкой - 1с.</p>
      <p>Сложно - Время между каждой кнопкой - 0.4с.</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    isStart: Boolean,
    difficulty: Number,
  },
  data() {
    return {
      difficultyArray: [
        {
          text: "Легко",
          value: 1500,
        },
        {
          text: "Нормально",
          value: 1000,
        },
        {
          text: "Сложно",
          value: 400,
        },
      ],
    };
  },
  methods: {
    startGame() {
      this.$emit("startGame");
    },
    updateDiffuclty(value) {
      this.$emit('update:difficulty', value)
    }
  },
};
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
.difficulty-description {
  margin-top: 40px;
  font-size: 16px;
  color: rgb(160, 160, 160);
}
</style>
