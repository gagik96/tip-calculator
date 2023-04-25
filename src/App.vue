<template>
  <div class="main-container">
    <div class="main-container__logo-container">
      <img class="main-container__logo-container__logo" src="./assets/logo.svg" alt="logo">
    </div>
    <Calculator />
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',

  components: {
    Calculator
  }
}
</script>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
}

#app {
  background-color: #C5E4E7;
  width: 100%;
  height: 100vh;
  font-family: 'Space Mono', monospace;
}

.main-container {
  display: flex;
}

.main-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;

  &__logo-container {
    width: 100%;
    display: flex;
    justify-content: center;
    margin-top: 170px;

    &__logo {
      width: 100px;
      height: 60px;
    }
  }
}
</style>
