<template>
  <div id="app">
    <TextEditorPage />
  </div>
</template>

<script>
import TextEditorPage from './components/TextEditorPage'
export default {
  name: 'App',
  components: {
    TextEditorPage
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
