<template>
  <div id="connection-block">
    <b-input-group prepend="Nom" class="mt-3">
      <b-form-input v-model="nom"></b-form-input>
    </b-input-group>
    <b-input-group prepend="Prénom" class="mt-3">
      <b-form-input v-model="prenom"></b-form-input>
    </b-input-group>
    <b-input-group prepend="Société" class="mt-3">
      <b-form-input v-model="nomSociete"></b-form-input>
    </b-input-group>
    <b-button class="buttonInfo" pill variant="info" @click="connected">Lancer le questionnaire</b-button>
  </div>
</template>

<script>
  export default {
    name: "Connexion",
    data() {
      return {
        nom: "",
        prenom: "",
        nomSociete: "",
        showError: false
      }
    },
    methods: {
      connected() {
        if (this.nom.trim() != "" && this.prenom.trim() != "" && this.nomSociete.trim() != "") {
          this.$router.push({
            path: '/questionnaire',
            query: {
              nom: this.nom,
              prenom: this.prenom,
              nomSociete: this.nomSociete
            }
          })

        } else {
          alert("Les champs doivent tous être remplis")
        }
      }
    }
  }
</script>

<style scoped>
  .buttonInfo{
    margin-top: 5%;
  }
</style>