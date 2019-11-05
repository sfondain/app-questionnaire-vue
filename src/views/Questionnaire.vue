<template>
  <div id="questionnaire">
    <h3>Bienvenue {{prenom}} {{nom}} de la société {{nomSociete}}</h3>
    <div id="question-component">
      <question :question="questions[counter]" @choice="choice = $event"></question>
      <b-button v-if="autreQuestion" block variant="outline-info" class="boutonConnexion" @click="questSuivante"><b>Question
        suivante</b>
      </b-button>
      <b-button v-else block variant="outline-success" class="boutonConnexion" @click="testFini">Terminer le test</b-button>
      <div class="erreur" v-if="erreur">Veuillez sélectionner une réponse</div>
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
        autreQuestion: true,
        choice: "",
        premier: true,
        resultats:[],
        score:0,
        erreur: false
      }
    },
    created() {
      this.questSuivante()
    },
    methods: {
      questSuivante() {
        if (this.choice != "" || this.premier) {
          this.erreur = false
          if (this.premier) {
            this.premier = false
          } else {
            let res = {
              'question': this.questions[this.counter],
              'choice': this.choice
            }
            this.resultats.push(res)
            this.isGoodAnswer()
            this.counter++
          }
          if (!this.questions[this.counter + 1]) {
            this.autreQuestion = false
          }
            this.choice = ""
          } else {
            this.erreur = true
          }
        },
      testFini() {
        if (this.choice != "") {
          let res = {
            'question': this.questions[this.counter],
            'choice': this.choice
          }
          this.resultats.push(res)
          this.isGoodAnswer()
          this.$router.push({
            path: 'score',
            query: {
              resultats: this.resultats,
              nom: this.nom,
              prenom: this.prenom,
              societe: this.nomSociete,
              score: this.score
            }
          })
        }
        else{
            this.erreur = true
        }
      },
      isGoodAnswer() {
        if (this.questions[this.counter].reponseExacte === this.choice) {
          this.score++
        }
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
  .boutonConnexion {
    height: 20%;
  }
  .erreur{
    color:red;
    grid-column: 2/4;
    margin:auto;
    text-align: center;
  }

</style>