<template>
  <div class="article">
    <h1>TWN artikkel</h1>
    <button v-on:click="loadApiData">Lae Api</button>
    <div v-if="responseAvailable">
      <hr>
      <p>
      <h1>{{ resultTitle }}</h1> <br>
      <h2>{{ resultIntro }}</h2>
      <br> <br>
      <img src="https://midaiganes.irw.ee/api/imgs/medium/344b02d7.jpg">
      <br> <br>
      <p2>{{ resultBody }}</p2>

      <hr>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwnArtikkel",
  data: function () {
    return {
      resultTitle: '',
      resultIntro: '',
      resultPicture: '',
      resultBody: '',
      responseAvailable: true,
    }
  },
  methods: {
    loadApiData: function () {
      this.$http.get("https://midaiganes.irw.ee/api/list/972d2b8a")
          .then(response => {
            this.resultTitle = response.data.title
            this.resultIntro = response.data.intro
            this.resultPicture = response.data.image.medium
            this.resultBody = response.data.body
            console.log(response.data.id)
            console.log(response.data.title)
          }).catch(error => {
        console.log(error)
      })
    }
  }
}
</script>

<style scoped>

</style>