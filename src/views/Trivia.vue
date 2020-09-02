<template>
  <div class="trivia">
      <div id='trivia-image'/>
    <trivia-round 
        v-if="!loading && !errored"
        :round=currentRound
        :key=currentRound.id
        :roundNum=currentRoundNum
    ></trivia-round>
  </div>
</template>

<script>
// @ is an alias to /src
import TriviaRound from '@/components/TriviaRound.vue'
import axios from 'axios'

export default {
  name: 'Trivia',

  components: {
    TriviaRound
  },

  data: function () {
    return {
        currentRoundNum: 1,
        // rounds: [
        //     {
        //         id: 1,
        //         type: 'visual',
        //         title: 'Creatures',
        //         numQuestions: 2
        //     },
        //     {
        //         id: 2,
        //         type: 'text',
        //         title: 'Something else',
        //         numQuestions: 0
        //     }
        // ],
        rounds: [],
        currentRound: null,
        roundUrl: 'https://emma-peterson-trivia.s3-us-west-1.amazonaws.com/metadata/round-metadata.json',
        loading: true,
        errored: false
    }
  },

    mounted() {
        axios
            .get(this.roundUrl)
            .then(response => {
                console.log(response.data)
                this.rounds = response.data.testArr
                this.currentRoundNum = response.data.currentRound
            })
            .catch(error =>  {
                this.errored = true
                console.log(error)
            })
            .finally(() => {
                this.currentRound = this.rounds[this.currentRoundNum-1]
                this.loading = false
            })
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