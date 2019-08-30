<template>
  <b-jumbotron class="card">
    <h4 class="question">
      You have completed the quiz.
      <br />
    </h4>
    <hr class="my-4" />
    <b-img :src="result[0]" class="img-fluid" alt="Responsive image"></b-img>
      <p class="question"> Result: {{numCorrect}} / 10</p>
      <p class="answer">{{result[1]}}</p>
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
        let result = [];
        if(this.numCorrect < 5){
            result.push('https://i.imgur.com/kLrG9IM.png');
            result.push('I love cheese, especially parmesan brie blue castello pepper jack fromage stinking bishop fromage frais dolcelatte smelly cheese. Cheese on toast squirty cheese, cheese and wine cheesy feet mascarpone danish fontina feta.');
        }else if(this.numCorrect <7){
            result.push('https://i.imgur.com/l8wAI21.png'); 
            result.push('I love cheese, especially parmesan brie blue castello pepper jack fromage stinking bishop fromage frais dolcelatte smelly cheese. Cheese on toast squirty cheese, cheese and wine cheesy feet mascarpone danish fontina feta.');
        }else if(this.numCorrect <=9){
            result.push('https://i.imgur.com/Qumjxfk.png');
            result.push('I love cheese, especially parmesan brie blue castello pepper jack fromage stinking bishop fromage frais dolcelatte smelly cheese. Cheese on toast squirty cheese, cheese and wine cheesy feet mascarpone danish fontina feta.');
        }else{
            result.push('https://i.imgur.com/DNyKZNC.png');
            result.push('I love cheese, especially parmesan brie blue castello pepper jack fromage stinking bishop fromage frais dolcelatte smelly cheese. Cheese on toast squirty cheese, cheese and wine cheesy feet mascarpone danish fontina feta.');
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
  width: 80%;
  margin-bottom: 30px;
  border-radius: 15px;
  color: rgba(0, 0, 0, 0.87);
  background: #fff;
  box-shadow: 0 10px 10px 0 rgba(0, 0, 0, 0.6),
    0 3px 1px -2px rgba(0, 0, 0, 0.6), 0 1px 5px 0 rgba(0, 0, 0, 0.6);
}
</style>