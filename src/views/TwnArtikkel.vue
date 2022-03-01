<template>
  <div class="article">
    <div class="grid-container">
      <div id="left"></div>
      <div v-if="responseAvailable" id="center">
        <div class="title">
          <h1>{{ resultTitle }}</h1>
        </div>
        <br>
        <div class="text">
          <h3 v-html="resultIntro"></h3>
          <br>
          <br>
          <img src="https://midaiganes.irw.ee/api/imgs/medium/344b02d7.jpg">
          <br>
          <br>
          <span v-html="resultBody"></span>
        </div>
      </div>
      <div id="right"></div>
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
            this.resultBody = response.data.body
            console.log(response.data.id)
            console.log(response.data.title)
          }).catch(error => {
        console.log(error)
      })
    }
  },
  beforeMount() {
    this.loadApiData()
  }
}
</script>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr;
  gap: 0px 0px;
  grid-template-areas:
    ". . .";
}

@font-face {
  font-family: "BoosterNextFY";
  src: url("/src/assets") format("woff2");
}

div.title {
  font-family: BoosterNextFY;
  text-transform: uppercase;
}

div.text {
  font-family: BoosterNextFY;
  text-align: center;
  text-align: justify;
  text-justify: inter-word;
}
</style>