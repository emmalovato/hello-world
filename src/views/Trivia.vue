<template>
  <div class="trivia">
    <!-- img alt="Trivia image" src="../assets/trivia.png" -->

      <div id='trivia-image'/>

    <trivia-round round="Test Round"/>
  </div>
</template>

<script>
// @ is an alias to /src
import TriviaRound from '@/components/TriviaRound.vue'

export default {
  name: 'Trivia',
  components: {
    TriviaRound
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#trivia-image {
  width: 300px;
  height: 177px;
  margin: 0 auto;
  background-size: contain;
  background-image: url('../assets/trivia.png');
}
</style>