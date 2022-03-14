<template>
  <div class="article">
    <div class="grid-container">
      <div id="left">
<!--        <img src="/src/assets/imgs/bg-deco-left.svg">-->
      </div>
      <div v-if="responseAvailable" id="center">
        <div class="title">
          <h1 style="color: #ffffff">{{ resultTitle }}</h1>
        </div>
        <br>
        <div class="text">
          <h3 v-html="resultIntro" style="color: #ffffff"></h3>
          <br>
          <br>
          <img src="https://midaiganes.irw.ee/api/imgs/medium/344b02d7.jpg">
          <br>
          <br>
          <span v-html="resultBody" style="color: #ffffff"></span>
        </div>
      </div>
      <div id="right">
<!--        <img src="/src/assets/imgs/bg-deco-right.svg">-->
      </div>
    </div>
    <button type="button" class="btn btn-danger">imperdiet</button>
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
  background: #3a3d57;
}

@font-face {
  font-family: "BoosterNextFY-Bold";
  src: url("/src/assets/BoosterNextFY-Bold.woff2") format("woff2");
}

div.title {
  font-family: BoosterNextFY-Bold;
  text-transform: uppercase;

}

div.text {
  font-family: BoosterNextFY-Bold;
  text-align: center;
  text-align: justify;
  text-justify: inter-word;
}

.article {
  background-image: url("/src/assets/imgs/bg-deco-left.svg"),url("/src/assets/imgs/bg-deco-right.svg");
  background-repeat: no-repeat;
  /*background-position: var(--twn-menuWidth) bottom,100% 0;*/
  background-size: 150px,250px;
  background-attachment: fixed;
  display: block;
  /*margin-left: var(--twn-menuWidth);*/
  height: 100vh;
  overflow: auto;
  padding: 5rem 2.5rem
}
</style>