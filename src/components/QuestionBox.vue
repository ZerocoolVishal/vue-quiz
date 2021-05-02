<template>
  <div class="question-box-container">
    <b-jumbotron lead="Bootstrap v4 Components for Vue.js 2">
      <template #lead>
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4">

      <b-row>
        <b-col md="6" offset-md="3">
          <b-list-group>
            <b-list-group-item
                v-for="(answer, index) in shuffleAnswers"
                :key="index"
                :class="{
                  'selected-ans': selectedIndex === index,
                  'correct-ans': (isSubmitted && index === correctIndex),
                  'incorrect-ans': (isSubmitted && selectedIndex === index && index !== correctIndex)
                }"
                :disabled="isSubmitted"
                @click="selectAnswer(index)">
              {{ answer }}
            </b-list-group-item>
          </b-list-group>
        </b-col>
      </b-row>

      <hr class="my-4">

      <b-button
          variant="primary"
          :disabled="selectedIndex === null || isSubmitted"
          @click="submitAnswer">
        Submit
      </b-button>

      <b-button
          class="ml-2"
          variant="success"
          @click="next">
        Next
      </b-button>

    </b-jumbotron>
  </div>
</template>

<script>
import _ from '../../node_modules/lodash';

export default {

  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function
  },

  data() {
    return {
      selectedIndex: null,
      shuffleAnswers: [],
      setValue: [],
      correctIndex: Number,
      isSubmitted: false
    }
  },

  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.isSubmitted = false;
        this.shuffleAnswer();
      }
    }
  },

  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
      if (this.currentQuestion.correct_answer === this.answers[index]) {
        console.log('Right !!');
      } else {
        console.log('Wrong !!');
      }
    },

    shuffleAnswer() {
      let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
      this.shuffleAnswers = _.shuffle(answers);
      this.correctIndex = this.shuffleAnswers.indexOf(this.currentQuestion.correct_answer);
    },

    submitAnswer() {
      // eslint-disable-next-line no-unused-vars
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.increment(isCorrect);
      this.isSubmitted = true;
    }
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    },
  }
}
</script>

<style scoped>
.list-group-item:hover {
  cursor: pointer;
  background-color: #f0f0f0;
}

.selected-ans {
  background-color: rgb(158, 158, 255) !important;
}

.correct-ans {
  background-color: rgb(137, 255, 137) !important;
}

.incorrect-ans {
  background-color: rgb(255, 115, 115) !important;
}
</style>
