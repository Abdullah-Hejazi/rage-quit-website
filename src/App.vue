<template>
  <div class="bg-blur">
    <h1 class="title">Rage Quit</h1>
    <p class="slogan">If you're gonna rage, do it right !</p>

    <RageBox />
  </div>
  
</template>

<script>
import RageBox from './components/RageBox.vue';

export default {
  name: 'App',

  components: {
    RageBox
  }
}
</script>

<style>
  @font-face {
    font-family: RosarivoRegular;
    src: url(assets/Rosarivo-Regular.ttf);
  }

  html { 
    background: url(assets/background.jpg) no-repeat center center fixed; 
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
    background-color: #0f0f0f;
    color: white;

    filter: progid:DXImageTransform.Microsoft.AlphaImageLoader(src='./assets/background.jpg', sizingMethod='scale');
    -ms-filter: "progid:DXImageTransform.Microsoft.AlphaImageLoader(src='assets/background.jpg', sizingMethod='scale')";
  }

  body {
    margin: 0px;
    padding: 0px;
  }

  .bg-blur {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgb(0,0,0);
    background-color: rgba(0,0,0,0.5);
  }

  .main {
    z-index: 5;
  }

  #app {
    font-family: RosarivoRegular, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  .title {
    text-align: center;
    font-size: 60px;
    margin: 50px auto 0px auto;
  }

  .slogan {
    text-align: center;
    margin: 10px auto;
  }

  @media only screen and (max-width: 400px) {
    .title {
      font-size: 35px;
    }
  }
</style>
