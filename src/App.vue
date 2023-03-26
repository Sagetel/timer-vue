<template>
  <div class="main">
    <TimerBlock v-for="index in timerBlocks" :key="index" />
    <div @click="addTimerBlock()" class="main__btn">
      <img src="/images/plusics.svg" alt="" srcset="" />
    </div>
  </div>
</template>

<script>
import TimerBlock from "./components/TimerBlock.vue";

export default {
  name: "App",
  components: {
    TimerBlock,
  },
  data() {
    return {
      timerBlocks: [],
    };
  },
  methods: {
    addTimerBlock() {
      this.timerBlocks.push({});
    },
  },
};
</script>

<style lang="scss">
@import "reset.css";
@import "../public/fonts/font.css";

html {
  font-family: "Gotham Pro Regular";
  height: 100vh;
  widows: 100vw;
  background-color: #353638;
  padding-top: 72px;
}
.main {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 50px 45px;
  flex-wrap: wrap;
  max-width: 775px;
  margin: 0 auto;

  @media (max-width: 800px) {
    max-width: 500px;
    grid-template-columns: repeat(2, 1fr);
  }

  @media (max-width: 540px) {
    max-width: 225px;
    grid-template-columns: 1fr;
  }

  &__btn {
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 225px;
    height: 120px;
    background: #696969;
    font-size: 20px;
    color: #9e9e9e;
  }
}
</style>
