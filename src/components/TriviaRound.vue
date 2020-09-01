<template>
  <div class="trivia-round">
    <h1>{{ round }}</h1>
    <h3>Question{{ questionNumTest }}</h3>
    <ul>
      <p>Question Text</p>
      <img alt="Question image" :src="imgUrl">
    </ul>
  </div>
</template>

<script>
module.exports = {
  
  name: 'TriviaRound',
  
  props: {
    round: String
  },
  
  data: function () {
    return {
      // textUrl: 'https://emma-peterson-trivia.s3-us-west-1.amazonaws.com/round-1/questions/text/q1.txt',
      imgUrl: 'https://emma-peterson-trivia.s3-us-west-1.amazonaws.com/round-1/questions/images/q1.png',
      questionNumTest: 1
    }
  },
  
  //created: function () {
    // `this` points to the vm instance
    //console.log('a is: ' + this.a)
  //}
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
</style>
