<template>
  <div id="app">
    <Header :numCorrect="numCorrect" :numTotal="numTotal" />
    <b-container>
      <b-row class="justify-content-center">
        <QuestionBox
          v-if="index < 10"
          :currentQuestion="questions[index]"
          :next="next"
          :increment="increment"
        />
        <Result :numCorrect="numCorrect" v-else />
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";
import Result from "./components/Result.vue";

export default {
  name: "app",
  components: {
    Header,
    QuestionBox,
    Result
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      componentKey: 0
    };
  },
  methods: {
    next() {
      this.index++;
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }
      this.numTotal++;
    }
  },
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=10&category=22&type=multiple", {
      method: "get"
    })
      .then(response => {
        return response.json();
      })
      .then(jsonData => {
        this.questions = jsonData.results;
      });
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Roboto|Roboto+Slab&display=swap");

#app {
  font-family: "Roboto Slab", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

html,
body,
#app {
  height: 100%;
  width: 100%;
  margin: 0px;
  padding: 0px;
  color: #fbfbfa;
  background-color: #30507a;
}

.question {
  color: #30507a;
  font-weight: 700;
  font-family: "Roboto Slab", "Times New Roman", serif;
  font: 18.2px;
}
.answer {
  font-family: "Roboto", "Helvetica", "Arial", sans-serif;
  font-weight: 300;
  line-height: 1.5em;
  color: #243853;
  font: 14px;
}

.card {
  display: inline-block;
  position: relative;
  width: 80%;
  margin-bottom: 30px;
  border-radius: 15px;
  color: rgba(0, 0, 0, 0.87);
  background: #fff;
  box-shadow: 0 10px 10px 0 rgba(0, 0, 0, 0.6),
    0 3px 1px -2px rgba(0, 0, 0, 0.6), 0 1px 5px 0 rgba(0, 0, 0, 0.6);
}

.list-group {
  margin-bottom: 15px;
}
</style>
