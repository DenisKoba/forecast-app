<template>
  <div id="app">
    <video autoplay muted loop id="myVideo">
      <source src="https://www.vidsplay.com/wp-content/uploads/2017/05/clouds2.mp4?_=1" type="video/mp4">
    </video>
    <city-forecast-component></city-forecast-component>
  </div>
</template>

<script>
  import cityForecastComponent from './components/cityForecastComponent'

  export default {
      name: 'App',
      components: {
          cityForecastComponent,
      },
      data() {
          return {
          }
      }
  }
</script>

<style lang="scss">
  * {
    padding: 0;
    margin: 0;
  }

  body {
    margin: 0;
  }

  #app {
    width: 100%;
  }
  video{
    position: fixed;
    right: 0;
    bottom: 0;
    min-width: 100%;
    min-height: 100%;
    z-index: -1;
  }
  .rain, .clouds {
    position: fixed;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    z-index: -1;
  }
  .multiselect{
    transform: scale(.97);
    position: relative;
    top: 5px;
  }

</style>
