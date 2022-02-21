<template>
  <div class="table">
    <h1>TWN tabel</h1>
    <button v-on:click="loadTableApiData">Lae Api</button>
    <div v-if = "responseAvailable">
      <hr>
      <p>
        <i>{{result}}</i>
      </p>
      <hr>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwnTabel",
  data: function () {
    return {
      result: '',
      responseAvailable: true,
    }
  },
  methods: {
    loadTableApiData: function () {
      this.$http.get("https://midaiganes.irw.ee/api/list?limit=500")
          .then(response => {
            this.result = response.data
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