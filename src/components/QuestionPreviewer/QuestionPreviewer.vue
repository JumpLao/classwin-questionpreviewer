<template>
  <div>
    <span v-for="token in tokens">
      <span v-if="token.type=='text'">
        {{token.value}}
      </span>
      <span v-if="token.type=='newline'">
        <br>
      </span>
      <span v-if="token.type=='image'">
        <img :src="token.value"/>
      </span>
      <equation-previewer v-if="token.type=='equation'" :expression="token.value" mode="latex">
      </equation-previewer>
      <graph-previewer v-if="token.type=='graph'" :expression="token.value">
      </graph-previewer>
      <span v-else>
        <component :is="token.type">{{token.value}}</component>
      </span>
      
    </span>
  </div>
</template>
<script>
import {EquationPreviewer} from './../EquationPreviewer'
import {GraphPreviewer} from './../GraphPreviewer'
export default {
  props: ['text'],
  components: {
    EquationPreviewer,
    GraphPreviewer
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
      let regex = /(?:<([^>]+)>([^<]*)<\/\1>|([^\s<>]+(?:[^\s<>]+)*)|(\n))/g
      while ((match = regex.exec(this.text)) !== null) {
        console.log(match)
        let token = {}
        if (match[1]) {
          token.type = match[1]
        } else if (match[3]) {
          token.type = 'text'
        } else if (match[4]) {
          token.type = 'newline'
        }
        token.value = match[2] || match[3] || match[4]
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
