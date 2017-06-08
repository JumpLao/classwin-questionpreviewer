<template>
  <span ref="previewer">
  </span>
</template>
<script>
import KaTex from 'katex'
import MathJS from 'mathjs'
import 'katex/dist/katex.min.css'
export default {
  props: ['expression', 'mode'],
  data () {
    return {}
  },
  mounted () {
    this.parse()
  },
  watch: {
    expression () {
      this.parse()
    }
  },
  methods: {
    parse () {
      try {
        let tex = this.expression
        if (this.mode !== 'latex') {
          tex = MathJS.parse(this.expression).toTex()
        }
        KaTex.render(tex || '', this.$refs.previewer)
      } catch (e) {
        console.log(e)
      }
    }
  }

}
</script>
<style lang='scss'>
</style>
