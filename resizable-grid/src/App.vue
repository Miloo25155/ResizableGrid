<template>
  <div id="app">
    <div id="container">
      <ResizableGrid></ResizableGrid>
      <!--<ResizableGrid scrollable></ResizableGrid>-->
    </div>
  </div>
</template>

<script>
import ResizableGrid from './components/ResizableGrid.vue'

export default {
  name: 'app',
  components: {
    ResizableGrid
  }
}
</script>

<style>
body{
  margin:0;
  padding: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color:  #2c3e50;
  width: 100vw;
  height:100vh;
  position:relative;
}

#container{
  position:absolute;
  top:50%;
  left:50%;
  transform: translate(-50%, -50%);
  width:75%;
  height:75%;
  margin: 0 auto;
  background-color: aliceblue;
  display:flex;
}
</style>
