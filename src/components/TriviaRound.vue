<template>
    <div class="trivia-round">
        <h1>Round {{ roundNum }}: {{ round.title }}</h1>
        <div v-for="q in questions" :key="q.id">
            <h3>Question {{ q.id }}</h3>
            <ul>
                <img alt="Question image" :src="`${baseImgUrl}/q${q.id}.png`">
                <p>{{ q.text }}</p>
            </ul>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'TriviaRound',
    
    props: {
        round: Object,
        // round: {
        //     id: Number,
        //     type: String,
        //     title: String,
        //     numQuestions: Number
        // },
        roundNum: Number
    },
    
    data: function () {
        return {
            baseImgUrl: `https://emma-peterson-trivia.s3-us-west-1.amazonaws.com/round-${this.roundNum}/questions/images`,
            baseTextUrl: `https://emma-peterson-trivia.s3-us-west-1.amazonaws.com/round-${this.roundNum}/questions/text`,
            questions: [],
            loading: true,
            errored: false
        }
    },

    // computed: {
    //     // this is an example for when I forget how to format this
    //     example: function () {
    //             return this.numbers.filter(function (number) {
    //                 return number % 2 === 0
    //         })
    //     }
    // },

    mounted() {
        let questionArr  = []
        for (let i=1; i<this.round.numQuestions+1; i++) {
            axios
                .get(`${this.baseTextUrl}/q${i}.txt`)
                .then(response => {
                    questionArr.push({
                            id: i,
                            text: response.data
                        })
                })
                .catch(error =>  {
                    this.errored = true
                    console.log(error)
                })
                .finally(() => this.loading = false)
        }
        this.questions = questionArr
    },

    // methods: {
    //     // this is an example for when I forget how to format this
    //     getQuestionText: function (questionNum) {
    //         var vm = this
    //         axios({ 
    //                 method: 'GET', 
    //                 url: `${this.baseTextUrl}/q${questionNum}.txt`
    //             })
    //             .then(result => {
    //                 // this.questionText = result.data
    //                 console.log(result.data)
    //                 vm.questionText = result.data
    //         }, error => {
    //             console.error(error);
    //             // this.questionText = 'Couldn\'t find question text'
    //             vm.questionText = 'Couldn\'t find question text'
    //         })
    //     }
    // }

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
