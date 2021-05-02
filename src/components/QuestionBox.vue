<template>
    <div class="question-box-container">
        <b-jumbotron lead="Bootstrap v4 Components for Vue.js 2"> 
                <template #lead>
                    {{ currentQuestion.question }}
                </template>

                <hr class="my-4">

                <b-list-group>
                    <b-list-group-item 
                        v-for="(answer, index) in answers" 
                        :key="index"
                        :class="{'selected-ans': selectedIndex === index}"
                        @click="selectAnswer(index)">
                        {{ answer }}
                    </b-list-group-item>
                </b-list-group>

                <hr class="my-4">

                <b-button variant="primary">Submit</b-button>
                <b-button class="ml-2" variant="success" @click="next">Next</b-button>
        </b-jumbotron>
    </div> 
</template> 

<script>
import _ from '../../node_modules/lodash';

export default {
    props: {
        currentQuestion: Object,
        next: Function
    },
    data() {
        return {
            selectedIndex: null,
            shuffleAnswers: []
        }
    },
    watch: {
        currentQuestion: {
            immediate: true,
            handler() {
                this.selectedIndex = null;
                let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
                this.shuffleAnswers = _.shuffle(answers);
            }
        }
    },
    methods: {
        selectAnswer(index) {
            this.selectedIndex = index;
            if (this.currentQuestion.correct_answer === this.answers[index]) {
                console.log('Right !!');
            }
            else {
                console.log('Wrong !!');
            }
        }
    },
    computed: {
        answers() {
            let answers = [...this.currentQuestion.incorrect_answers];
            answers.push(this.currentQuestion.correct_answer);
            return answers;
        }
    }
}
</script>

<style scoped>
    .list-group-item:hover {
        cursor: pointer;
        background-color: #f0f0f0;
    }
    .selected-ans {
        background-color: rgb(158, 158, 255);
    }
    .correct-ans {
        background-color: rgb(137, 255, 137);
    }
    .incorrect-ans {
        background-color: rgb(255, 115, 115);
    }
</style>