<template>
  <div id="app">
    <Header 
      :numCorrect="numCorrect"
      :numTotal="numTotal"
    />
    <b-container>
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox 
          v-if="questions.length && index < 10"
          :currentQuestion="questions[index]" 
          :next="next"
          :increment="increment"
          />
          <Result 
          :numCorrect="numCorrect"
          v-else/>
        </b-col>
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
    next(){
      this.index++;
    },
    increment(isCorrect){
      if(isCorrect){
        this.numCorrect++;
      }
      this.numTotal++;
    }
  },
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=10&category=18&type=multiple", {
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
#app {
  font-family: "Roboto Slab", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #FBFBFA;
  background-color: #30507A;
  height: 100%;
}
body {
  height: 100vh;
  margin: 0;
  padding: 0px;
  
  width: 100%;
}
</style>
