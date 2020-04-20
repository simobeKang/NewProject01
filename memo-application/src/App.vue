<template>
  <div id="app">
    <app-header />
    <memo-app />
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import MemoApp from "./components/MemoApp.vue";

export default {
  name: "app",
  components: {
    AppHeader,
    MemoApp
  }
};
</script>

<style>
@import "./style/reset.css";
#app {
  width: 560px;
  margin: 0 auto;
}

body {
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: #031321;
  font-family: consolas;
}
</style>
