<template>
  <button
    class="circle__part"
    :class="
      `circle__part--${item.id} ${activeItem === item.id ? 'active' : ''}`
    "
    @click="playSound(item.id)"
    :disabled="isDisableButton"
  ></button>
</template>

<script>
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
  props: {
    item: Object,
    activeItem: Number,
    isDisableButton: Boolean,
  },
  methods: {
    playSound(id) {
      this.$emit("update:userChain", id);
      switch (id) {
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
};
</script>

<style>
.circle__part {
  width: 200px;
  height: 200px;
  border: none;
  outline: none;
  cursor: pointer;
  transition: all 0.1s linear;
}
.circle__part:disabled {
  cursor: initial;
}
/* Верхний левый круг */
.circle__part--1 {
  background-color: #11998e;
}
.circle__part--1:hover,
.circle__part--1:focus {
  background-color: #0e7a71;
}
.circle__part--1:active,
.circle__part--1.active {
  background-color: #15bbad;
}
/* Верхний правый круг */
.circle__part--2 {
  background-color: #2193b0;
}
.circle__part--2:hover,
.circle__part--2:focus {
  background-color: #19758b;
}
.circle__part--2:active,
.circle__part--2.active {
  background-color: #25acce;
}
/* Нижний левый круг */
.circle__part--3 {
  background-color: #ff4b2b;
}
.circle__part--3:hover,
.circle__part--3:focus {
  background-color: #cc3d23;
}
.circle__part--3:active,
.circle__part--3.active {
  background-color: #f76f6f;
}
/* Нижний правый круг */
.circle__part--4 {
  background-color: #b06ab3;
}
.circle__part--4:hover,
.circle--part--4:focus {
  background-color: #925794;
}
.circle__part--4:active,
.circle__part--4.active {
  background-color: #d27ed4;
}
</style>
