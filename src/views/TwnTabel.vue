<template>
  <div class="table">
    <h1>NIMEKIRI</h1>
    <div class="grid-container">
      <div id="left"></div>
      <div id="api">
        <table class="table table-striped">
          <thead>
          <tr>
            <th @click="sort('user.firstname')">Eesnimi</th>
            <th>Perekonnanimi</th>
            <th>Sugu</th>
            <th>Sünnikuupäev</th>
            <th>Telefon</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="user in list">
            <td>{{ user.firstname }}</td>
            <td>{{ user.surname }}</td>
            <td>
              <template v-if="user.sex == 'f'">Naine</template>
              <template v-else>Mees</template>
            </td>
            <td>{{ user.personal_code }}</td>
            <td>{{ user.phone }}</td>
          </tr>
          </tbody>
        </table>
      </div>
      <div id="right"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwnTabel",
  data: function () {
    return {
      result: '',
      list: {},
    }
  },
  methods: {
    loadTableApiData: function () {
      this.$http.get("https://midaiganes.irw.ee/api/list?limit=500")
          .then(response => {
            this.list = response.data.list
            console.log(response.data)
          }).catch(error => {
        console.log(error)
      })
    },
  },
  beforeMount() {
    this.loadTableApiData()
  },
}
</script>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: 1fr 1.5fr 1fr;
  grid-template-rows: 1fr;
  gap: 0px 0px;
  grid-template-areas:
    ". . .";
}
</style>