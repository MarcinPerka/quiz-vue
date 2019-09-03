<template>
  <b-jumbotron class="card">
    <h4 class="question">
      You have completed the quiz.
      <br />
    </h4>
    <hr class="my-4" />
    <div class="text-center">
      <b-img :src="result[0]" class="img img-fluid" alt="Responsive image"></b-img>
    </div>
    <p class="question">Result: {{numCorrect}} / 10</p>
    <p class="answer">{{result[1]}}</p>
    <b-button pill class="btn-success" @click="reloadPage">Play again</b-button>
  </b-jumbotron>
</template>

<script>
export default {
  props: {
    numCorrect: Number
  },
  methods: {
    reloadPage() {
      window.location.reload();
    }
  },
  computed: {
    result: function() {
      let result = [];
      if (this.numCorrect < 5) {
        result.push("https://i.imgur.com/kLrG9IM.png");
        result.push(
          "I love cheese, especially parmesan brie blue castello pepper jack fromage stinking bishop fromage frais dolcelatte smelly cheese. Cheese on toast squirty cheese, cheese and wine cheesy feet mascarpone danish fontina feta."
        );
      } else if (this.numCorrect < 7) {
        result.push("https://i.imgur.com/l8wAI21.png");
        result.push(
          "I love cheese, especially parmesan brie blue castello pepper jack fromage stinking bishop fromage frais dolcelatte smelly cheese. Cheese on toast squirty cheese, cheese and wine cheesy feet mascarpone danish fontina feta."
        );
      } else if (this.numCorrect <= 9) {
        result.push("https://i.imgur.com/Qumjxfk.png");
        result.push(
          "I love cheese, especially parmesan brie blue castello pepper jack fromage stinking bishop fromage frais dolcelatte smelly cheese. Cheese on toast squirty cheese, cheese and wine cheesy feet mascarpone danish fontina feta."
        );
      } else {
        result.push("https://i.imgur.com/DNyKZNC.png");
        result.push(
          "I love cheese, especially parmesan brie blue castello pepper jack fromage stinking bishop fromage frais dolcelatte smelly cheese. Cheese on toast squirty cheese, cheese and wine cheesy feet mascarpone danish fontina feta."
        );
      }
      return result;
    }
  }
};
</script>

<style scoped>

.img{
  min-width: 64px;
  max-width: 256px;
  max-height: 256px;
  min-height: 64px;
}
</style>

