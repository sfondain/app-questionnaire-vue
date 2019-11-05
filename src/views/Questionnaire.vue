<template>
  <div id="questionnaire">
    <h3>Bienvenue {{prenom}} {{nom}} de la société {{nomSociete}}</h3>
    <div id="question-component">
      <question :question="questions[counter]" @choice="choice = $event"></question>
      <b-button v-if="canNextQuestion" block variant="outline-info" class="connectButton" @click="nextQuestion"><b>Question
        suivante</b>
      </b-button>
      <b-button v-else block variant="outline-success" class="connectButton" @click="testFinish">Terminer le test</b-button>
    </div>
  </div>
</template>

<script>
  import questionsJSON from '../assets/questions.json'
  import Question from "../components/Question";
  export default {
    name: "Questionnaire",
    components: {
      Question
    },
    data() {
      return {
        nom: this.$route.query.nom,
        prenom: this.$route.query.prenom,
        nomSociete: this.$route.query.nomSociete,
        questions: questionsJSON.questions,
        counter: 0,
        canNextQuestion: true,
        choice: "",
        first: true
      }
    },
    created() {
      this.nextQuestion()
    },
    methods: {
      nextQuestion() {
        if (this.first) {
          this.first = false
        } else {
          this.counter++
        }
        if (!this.questions[this.counter + 1]) {
          this.canNextQuestion = false
        }
      },
      testFinish() {
      }
    }
  }
</script>

<style scoped>
  #questionnaire {
    height: 100%;
    display: grid;
    grid-template-columns: 15% 35% 35% 15%;
    grid-template-rows: 15% 35% 35% 15%;
    background-color: aliceblue;
  }
  h3 {
    grid-row: 1/2;
    grid-column: 2/4;
    margin:auto;
  }
  #question-component {
    background-color: white;
    border-radius: 20px;
    grid-row: 2/4;
    grid-column: 2/4;
  }
  .connectButton {
    height: 20%;
  }

</style>