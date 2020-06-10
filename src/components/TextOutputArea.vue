<template>
  <div class="textarea__output">
    <h2>Here is your text.</h2>
    <TextOutputItem 
      v-for="item of styledText"
      v-bind:item="item"
      v-bind:key="item.id"
    />
  </div>
</template>

<script>
import TextOutputItem from './TextOutputItem'
export default {
  props: ['styledText'],
  components: {
    TextOutputItem
  }
}
</script>

<style>

</style>