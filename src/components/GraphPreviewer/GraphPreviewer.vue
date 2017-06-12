<template>
  <div :id="`graph-${uuid}`"></div>
</template>
<script>
import * as d3 from 'd3'
export default {
  props: ['expression'],
  data () {
    return {
      uuid: ''
    }
  },
  created () {
    window.d3 = d3
    this.uuid = 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function (c) {
      let r = Math.random() * 16 | 0
      let v = c === 'x' ? r : (r & 0x3 | 0x8)
      return v.toString(16)
    })
  },
  watch: {
    expression () {
      this.drawGraph()
    }
  },
  mounted () {
    this.drawGraph()
  },
  methods: {
    drawGraph () {
      let self = this
      let functionPlot = require('function-plot')
      if (self.expression) {
        try {
          functionPlot({
            target: `#graph-${this.uuid}`,
            data: [{
              fn: self.expression
            }]
          })
        } catch (err) {
          console.log(err)
        }
      }
    }
  }
}
</script>
<style lang='scss'>
</style>
