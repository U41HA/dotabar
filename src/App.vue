<template>
  <div id="app">
    <HealthBar />
    <!-- <HealthBar :health-count="healthCount" /> -->
    <!-- <div class="buttons">
      <HitButtons :button-text="'Hit'"/>
      <HitButtons :button-text="'Heal'"/>
    </div> -->
    
  </div>
</template>

<script>

// import HelloWorld from './components/HelloWorld.vue'
import HealthBar from './components/HealthBar.vue';

export default {
  name: 'App',

  components: {
    HealthBar,
  },

  data() {
    return {
      msg: "Hello, there!",
      // healthCount: 1800,
    }
  }
}

</script>

<style lang="scss">
body {
  margin: 0;
}

#app {
  @font-face {
    font-family: Trajan;
    src:
      url(../src/assets/fonts/TrajanBold.woff2) format(woff2),
      url(../src/assets/fonts/TrajanBold.ttf) format(ttf);
    font-style: bold;
    font-variant: normal;
  }

  font-family: 'Trajan';
  font-size: 10px;
  font-weight: bold;
  color: $color-interface;
  
  padding: 50px 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 50px;

  background: url(../src/assets/image/background.jpeg) center center no-repeat;
  background-size: cover;
  box-sizing: border-box;
  min-height: 100vh;
}

.buttons {
  display: flex;
  gap: 30px;
}
</style>
