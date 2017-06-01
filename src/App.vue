<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>

body {
    background: url('assets/background.jpg')center no-repeat;
    background-color: #000;
    background-size: 100% 100%;
}
.bgForm {
    background: url('assets/bg-form.png');
}
.bgForm2 {
    background: url('assets/bg-form2.png');
}
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 20px auto 0 auto;
  width: 90%;
  /*max-width: 1100px;*/
}
</style>
