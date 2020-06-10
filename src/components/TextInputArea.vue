<template>
  <div class="textarea__wraper">
    <div class="textarea__buttons">
      <label>
        Color
        <input
          type="color"
          v-model="color"
        >
      </label>
      <label>
        Background Color
        <input
          type="color"
          v-model="backgroundColor"
        >
      </label>
      <label>
        Font size
        <input
          type="number"
          min="1"
          max="52"
          v-model="fontSize"
        >
      </label>
    </div>
    <textarea
      v-model="text"
      cols="30"
      rows="10"
      @select="getSelectedValues"
    ></textarea>

    <TextOutputArea 
      v-bind:styledText="textArrOfObjects"
    />
  </div>
</template>

<script>
import TextOutputArea from './TextOutputArea'
export default {
  name: 'TextInputArea',
    methods: {
      getSelectedValues(event) {
        const arrayOfData = this.arrayOfPositionsTextSelection
        const { selectionStart, selectionEnd } = event.target
        if (arrayOfData.length === 1 && arrayOfData[0].start > selectionStart) {
          arrayOfData.pop()
        }
        if (arrayOfData.length > 1) {
          this.arrayOfPositionsTextSelection = arrayOfData.map(element => {
            if (element.start <= selectionStart) {
              return element
            }
          })
        }
        if (arrayOfData.length > 1) {
          if(arrayOfData[arrayOfData.length - 1].end > selectionStart) {
            this.arrayOfPositionsTextSelection[arrayOfData.length - 1].end = selectionStart
          }
        }
        if(arrayOfData.length >= 1) {
          if(arrayOfData[arrayOfData.length - 1].end < selectionStart) {
            arrayOfData.push({
              start: arrayOfData[arrayOfData.length - 1].end,
              end: selectionStart,
              color: '#000000',
              background: '#ffffff',
              fontSize: "12",
            })
          }
        }
        arrayOfData.push({
          start: selectionStart,
          end: selectionEnd,
          color: this.color,
          background: this.backgroundColor,
          fontSize: this.fontSize
        })
        this.setTextArrOfObjects()
      },

      setTextArrOfObjects() {
        const arrayOfData = this.arrayOfPositionsTextSelection
        let id = 0
        this.textArrOfObjects = arrayOfData.map(element => {
          let {color, background, fontSize, start, end} = element
          const text = this.textArr.slice(start, end).join('')
          return ({
            color: color,
            background: background,
            fontSize: fontSize,
            text: text
          })
        })

        if (arrayOfData[0].start > 0) {
          this.textArrOfObjects.unshift({
            color: '#000000',
            backgroundColor: '#ffffff',
            fontSize: "12",
            text: this.textArr.slice(0, arrayOfData[0].start).join('')
          })
        }

        if (arrayOfData[arrayOfData.length - 1].end < this.textArr.length) {
          this.textArrOfObjects.push({
            color: '#000000',
            backgroundColor: '#ffffff',
            fontSize: "12",
            text: this.textArr.slice(arrayOfData[arrayOfData.length - 1].end, this.textArr.length).join('')
          })
        }
        this.arrayOfPositionsTextSelection = this.arrayOfPositionsTextSelection.map(item => {
          id += id + 1
          return ({
            ...item,
            id: id
          })
        })
      }
  },

  data() {
    return {
      text: '',
      color: '#000000',
      backgroundColor: '#ffffff',
      fontSize: "12",
      textArr: [],
      textArrOfObjects: [],
      arrayOfPositionsTextSelection: []
    }
  },
  watch: {
    'text': function() {
      this.textArr = this.text.split('')
    },
  },
  components: {
    TextOutputArea
  }
}
</script>

<style>

</style>