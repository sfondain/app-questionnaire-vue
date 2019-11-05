<template>
    <div id="questionnaire">
        <h3>Bienvenue {{prenom}} {{nom}} de la société {{societe}}</h3>
        <div class="score ">
            <div v-for="(res, index) in resultats" class="score" :key="index">
                <span :class="question">{{res.question.question}}</span>
                <span class="reponse" :class="res.choice == res.question.reponseExacte ? 'green':'red'"> {{res.choice}}</span> <span class="font-weight-bold" v-if="res.choice != res.question.reponseExacte" > (La réponse exacte était : {{res.question.reponseExacte}}) </span>
            </div>
            <span class="resultatfinal">Score {{score}}/{{resultats.length}}</span>
        </div>
    </div>
</template>

<script>
    export default {
        name: "score",
        data() {
            return {
                nom: this.$route.query.nom,
                prenom: this.$route.query.prenom,
                societe: this.$route.query.societe,
                resultats: this.$route.query.resultats,
                score: this.$route.query.score
            }
        },
        methods: {
        }
    }
</script>

<style scoped>
    #questionnaire {
        height: 100%;
        display: grid;
        grid-template-columns: 15% 35% 35% 15%;
        grid-template-rows: 15% 35% 35% 15%;
        background-color: lightblue;
    }
    h3 {
        grid-row: 1/2;
        grid-column: 1/4;
    }
    .score {
        background-color: white;
        border-radius: 20px;
        grid-row: 2/4;
        grid-column: 2/4;
    }
    .green{
        color:green;
    }
    .red{
        color:red;
    }
    .resultatfinal{
        font-weight: bold;
        font-size: larger;
        margin:auto;
        grid-column: 1/2;
    }
</style>