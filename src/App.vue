<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" width="25%"> -->
    <!-- <HelloWorld msg="Hello Vue in CodeSandbox!"/> -->
  <todo />
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld";
import todo from "./components/todo";
export default {
  name: "App",
  components: {
    todo
    // HelloWorld
  }
};
</script>

<style>
#app {
  font-size: 16px;
  font-family: Verdana, sans-serif;
}
</style>
