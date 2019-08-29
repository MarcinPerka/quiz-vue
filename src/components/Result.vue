<template>
  <b-jumbotron class="card">
    <h4 class="question">
      You have completed the quiz.
      <br />
    </h4>
    <hr class="my-4" />
    <b-list-group>
      <b-list-group-item class="answer">{{result}}</b-list-group-item>
    </b-list-group>
    <b-button pill class="btn-success" @click="reloadPage">Play again</b-button>
  </b-jumbotron>
</template>

<script>

export default {
  props: {
    numCorrect: Number,
  },
  methods:{
      reloadPage(){
          window.location.reload()
      }
  },
  computed: {
    result: function() {
        let result = '';
        if(this.numCorrect < 5){
            result = 'You need to pratice';
        }else if(this.numCorrect <7){
            result = 'It is a good result';
        }else if(this.numCorrect <=9){
            result = 'Woah';
        }else{
            result = 'You are nerd';
        }
      return result;
    }
  },
};
</script>

<style scoped>
.list-group {
  margin-bottom: 15px;
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
  width: 100%;
  margin-bottom: 30px;
  border-radius: 15px;
  color: rgba(0, 0, 0, 0.87);
  background: #fff;
  box-shadow: 0 10px 10px 0 rgba(0, 0, 0, 0.6),
    0 3px 1px -2px rgba(0, 0, 0, 0.6), 0 1px 5px 0 rgba(0, 0, 0, 0.6);
}
</style>