<template>
  <div class="game-wrapper">
    <div class="main-circle">
      <CirclePart
        v-for="item in items"
        :key="item.id"
        :item="item"
        :activeItem="activeItem"
        :isDisableButton="isDisableButton"
        @update:userChain="updateUserChain"
      />
    </div>
    <GameOptions
      @startGame="start"
      :isStart="isStart"
      :difficulty="difficulty"
      @update:difficulty="updateDifficulty"
    />
  </div>
</template>

<script>
import CirclePart from "./CirclePart";
import GameOptions from "./GameOptions";

const srcAudioOne = require("../assets/sounds/1.ogg");
const srcAudioTwo = require("../assets/sounds/2.ogg");
const srcAudioThree = require("../assets/sounds/3.ogg");

const audioOne = new Audio(srcAudioOne);
const audioTwo = new Audio(srcAudioTwo);
const audioThree = new Audio(srcAudioThree);
const audioFour = new Audio(
  "https://s3.amazonaws.com/freecodecamp/simonSound4.mp3"
);

export default {
  data() {
    return {
      chain: [],
      userChain: [],
      activeItem: null,
      isDisableButton: true,
      step: 0,
      isStart: false,
      items: [
        {
          id: 1,
        },
        {
          id: 2,
        },
        {
          id: 3,
        },
        {
          id: 4,
        },
      ],
      difficulty: 1500,
    };
  },
  methods: {
    start() {
      this.isStart = true;
      this.pushRandomId();
      this.startTheGame();
    },
    pushRandomId() {
      const id = Math.floor(Math.random() * 4) + 1;
      this.chain.push(id);
    },
    updateDifficulty(value) {
      this.difficulty = value;
    },
    startTheGame(index = 0) {
      if (!this.isDisableButton) {
        return;
      }
      this.activeItem = this.chain[index];

      setTimeout(() => {
        this.activeItem = null;
      }, 500);

      if (this.step === index) {
        this.isDisableButton = false;
        return;
      }

      setTimeout(() => {
        this.startTheGame(index + 1);
      }, this.difficulty);
    },
    updateUserChain(id) {
      this.userChain.push(id);
      const isEqual = arrayIsEqual(this.chain, this.userChain);

      if (!isEqual) {
        this.isDisableButton = true;
        this.chain = [];
        this.userChain = [];
        this.step = 0;
        this.isStart = false;
        return;
      }

      if (this.chain.length === this.userChain.length) {
        this.userChain = [];
        this.step++;
        this.isDisableButton = true;
        this.pushRandomId();
        setTimeout(() => {
          this.startTheGame();
        }, 1000);
      }
    },
    stopAudio() {
      audioOne.pause();
      audioOne.currentTime = 0;
      audioTwo.pause();
      audioTwo.currentTime = 0;
      audioThree.pause();
      audioThree.currentTime = 0;
      audioFour.pause();
      audioFour.currentTime = 0;
    },
  },
  watch: {
    activeItem(val) {
      switch (val) {
        case 1:
          this.stopAudio();
          audioOne.play();
          break;
        case 2:
          this.stopAudio();
          audioTwo.play();
          break;
        case 3:
          this.stopAudio();
          audioThree.play();
          break;
        case 4:
          this.stopAudio();
          audioFour.play();
          break;
        default:
          break;
      }
    },
  },
  components: {
    CirclePart,
    GameOptions,
  },
};

const arrayIsEqual = (a, b) => {
  if (b.length > a.length) {
    return false;
  }
  for (let i = 0; i < b.length; i++) {
    if (b[i] !== a[i]) {
      return false;
    }
  }
  return true;
};
</script>

<style>
.game-wrapper {
  display: flex;
}
.main-circle {
  display: flex;
  flex-wrap: wrap;
  width: 400px;
  height: 400px;
  background-color: white;
  border-radius: 50%;
  overflow: hidden;
}
</style>
