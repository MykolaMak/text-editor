<template>
  <div class="editor__wraper">
    <div class="editor__input-text">
      <h1>Please, input your text.</h1>
      <h2>Then choose <em>color, background, font-size</em>.</h2>
      <h3>After then select text which you want to style.</h3>
      <TextInputArea />
    </div>
  </div>
</template>

<script>
import TextInputArea from './TextInputArea'
export default {
  components: {
    TextInputArea
  }
}
</script>

<style>

</style>