<template>
  <div class="hello">
    <textarea v-model="question"></textarea>
    <question-previewer :text="question"></question-previewer>
    <!-- <equation-previewer :expression="expression" mode='latex'></equation-previewer> -->
  </div>
</template>

<script>
import {EquationPreviewer} from './EquationPreviewer'
import {QuestionPreviewer} from './QuestionPreviewer'
export default {
  components: {
    EquationPreviewer,
    QuestionPreviewer
  },
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      expression: '',
      question: ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
