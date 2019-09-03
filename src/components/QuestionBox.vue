<template>

  <b-jumbotron class="card">
    <h4 class="question" v-html="currentQuestion.question"></h4>
    <hr class="my-4" />
    <b-list-group class="answer">
       <b-list-group-item
        v-for="(answer, index) in answers"
        :key="index"
        @click.prevent="selectAnswer(index)"
        :class="answerClass(index)"
        v-html="answer"
      ></b-list-group-item>
    </b-list-group>
        <b-button-group class="mt-2"> 
    <b-button
      pill
      class="btn-success btn-md button-width"
      @click="submitAnswer"
      :disabled="selectedIndex === null || answered"
    >Submit</b-button>
    <b-button pill class="btn-info btn-md button-width" @click="next" :disabled="answered === false">Next</b-button>
          </b-button-group>
  </b-jumbotron>
</template>

<script>
import _ from "lodash";

export default {
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function,
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffledAnswers: [],
      answered: false
    };
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.answered = false;
        this.shuffleAnswers();
      }
    }
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    submitAnswer() {
      let isCorrect = false;

      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.answered = true;
      this.increment(isCorrect);
    },
    shuffleAnswers() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer
      ];
      this.shuffledAnswers = _.shuffle(answers);
      this.correctIndex = this.shuffledAnswers.indexOf(
        this.currentQuestion.correct_answer
      );
    },
    answerClass(index) {
      let answerClass = "";

      if (!this.answered && this.selectedIndex === index) {
        answerClass = "selected";
      } else if (this.answered && this.correctIndex === index) {
        answerClass = "correct";
      } else if (
        this.answered &&
        this.selectedIndex === index &&
        this.correctIndex !== index
      ) {
        answerClass = "incorrect";
      }

      return answerClass;
    }
  }
};
</script>

<style scoped>

.list-group-item:hover {
  background: #eee;
  cursor: pointer;
}
.btn {
  margin: 0 5px;
}

.selected {
  background-color: #949ba2;
}
.selected:hover{
  background-color: #949ba2;
}
.correct {
  background-color: #62a969;
}
.correct:hover{
  background-color: #62a969;
}
.incorrect{
  background-color: #f44336;
}
.incorrect:hover{
  background-color: #f44336;
}

.button-width{
  width: 78px !important;
}

</style>