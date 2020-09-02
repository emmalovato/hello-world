<template>
  <div class="trivia">
      <div id='trivia-image'/>
    <trivia-round 
        v-for="(round, index) in rounds"
        :round=round
        :key=round.id
        :roundNum="index + 1"
    ></trivia-round>
  </div>
</template>

<script>
// @ is an alias to /src
import TriviaRound from '@/components/TriviaRound.vue'

export default {
  name: 'Trivia',
  components: {
    TriviaRound
  },
  data: function () {
    return {
        rounds: [
            {
                id: 1,
                type: 'visual',
                title: 'Creatures',
                numQuestions: 2
            },
            {
                id: 2,
                type: 'text',
                title: 'Something else',
                numQuestions: 0
            }
        ]
    }
  },
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