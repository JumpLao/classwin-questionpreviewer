<template>
  <div>
    <span v-for="token in tokens">
      <span v-if="token.type=='text'">
        {{token.value}}
      </span>
      <equation-previewer v-if="token.type=='equation'" :expression="token.value" mode="latex">
      </equation-previewer>
    </span>
  </div>
</template>
<script>
import {EquationPreviewer} from './../EquationPreviewer'
export default {
  props: ['text'],
  components: {
    EquationPreviewer
  },
  data () {
    return {
    }
  },
  computed: {
    tokens () {
      // let self = this
      let match
      let results = []
      let regex = /(?:<([^>]+)>([^<]*)<\/\1>|([^\s<>]+(?:[\s]*[^\s<>]+)*))/g
      while ((match = regex.exec(this.text)) !== null) {
        console.log(match)
        let token = {}
        if (match[1]) {
          token.type = match[1]
        } else {
          token.type = 'text'
        }
        token.value = match[2] || match[3]
        results.push(token)
      }
      return results
    }
  },
  methods: {
    encodeHtml (text) {
      return text.replace(/&/g, '&amp;amp;')
      .replace(/</g, '&lt;')
      .replace(/>/g, '&gt;')
      .replace(/"/g, '&quot;')
      .replace(/'/g, '&apos')
    }
  }
}
</script>
<style lang='scss'>
</style>
