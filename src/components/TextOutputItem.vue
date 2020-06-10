<template>
  <span v-bind:style="styledObject">{{ item.text }}</span>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      textArr: this.item.text.split('\n'),
      styledObject: {
        color: this.item.color,
        backgroundColor: this.item.background,
        fontSize: this.item.fontSize + 'px',
      }
    }
  }
}
</script>

<style>

</style>