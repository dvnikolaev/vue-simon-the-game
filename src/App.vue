<template>
  <div id="app">
    <MainCircle />
  </div>
</template>

<script>
import MainCircle from "./components/MainCircle";

export default {
  name: "App",
  components: {
    MainCircle,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
.page__body {
  display: flex;
  justify-content: center;
  align-items: center;
  background: #dae2f8; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to bottom,
    #d6a4a4,
    #dae2f8
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to bottom,
    #d6a4a4,
    #dae2f8
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  margin: 0;
  min-height: 100vh;
}
</style>
