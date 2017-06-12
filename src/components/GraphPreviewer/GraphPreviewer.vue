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
    expression (val) {
      this.drawGraph(val)
    }
  },
  mounted () {
    this.drawGraph('x=0')
    this.drawGraph(this.expression)
  },
  methods: {
    drawGraph (expression) {
      let functionPlot = require('function-plot')
      if (expression) {
        try {
          functionPlot({
            target: `#graph-${this.uuid}`,
            data: [{
              fn: expression,
              sampler: 'builtIn',
              graphType: 'polyline'
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
