<template>
  <div id="app">
    <Header
      :num-correct="numCorrect"
      :num-total="numTotal"
    />
    <QuestionBox 
      v-if="questions.length"
      :current-question="questions[index]"
      :next="nextQuestion"
      :increment="increment"
    />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0
    }
  },
  methods: {
    nextQuestion() {
      this.index++;
      // if (this.index === (this.questions.length)) {
      //   this.index = 0;
      // }
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }
      this.numTotal++;
    }
  },
  mounted: function() {
     fetch('https://opentdb.com/api.php?amount=10&type=multiple', {
       method: 'get'
     }).then((response) => {
      return (response.json());
     }).then((data) => {
      // console.log(data);
      this.questions = data.results;
     });
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
