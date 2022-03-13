<template>
  <div class="table">
    <h1>NIMEKIRI</h1>
    <div class="grid-container">
      <div id="left"></div>
      <div id="api">
        <table class="table table-striped">
          <thead>
          <tr>
            <th v-on:click="sort('user.firstname')">Eesnimi</th>
            <th @click="sort('user.surname')">Perekonnanimi</th>
            <th @click="sort('user.sex')">Sugu</th>
            <th @click="sort('user.birthday')">Sünnikuupäev</th>
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
        <nav aria-label="Table pages">
          <ul class="pagination">
            <li class="page-item">
              <a class="page-link" href="#" aria-label="Previous">
                <span aria-hidden="true">&laquo;</span>
                <span class="sr-only">Previous</span>
              </a>
            </li>
            <li class="page-item"><a class="page-link" href="#">1</a></li>
            <li class="page-item"><a class="page-link" href="#">2</a></li>
            <li class="page-item"><a class="page-link" href="#">3</a></li>
            <li class="page-item">
              <a class="page-link" href="#" aria-label="Next">
                <span aria-hidden="true">&raquo;</span>
                <span class="sr-only">Next</span>
              </a>
            </li>
          </ul>
        </nav>
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
      // result: '',
      list: {},
      currentSort: 'firstname',
      currentSortDir: 'asc',
      pageSize: 10,
      currentPage: 1
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
    sort: function (s) {
      //if s == current sort, reverse
      if (s === this.currentSort) {
        this.currentSortDir = this.currentSortDir === 'asc' ? 'desc' : 'asc';
      }
      this.currentSort = s;
    },
    nextPage:function() {
      if((this.currentPage*this.pageSize) < this.list.length) this.currentPage++;
    },
    prevPage:function() {
      if(this.currentPage > 1) this.currentPage--;
    }
  },
  computed: {
    sortedNames: function () {
      return this.list.sort((a, b) => {
        let modifier = 1;
        if (this.currentSortDir === 'desc') modifier = -1;
        if (a[this.currentSort] < b[this.currentSort]) return -1 * modifier;
        if (a[this.currentSort] > b[this.currentSort]) return 1 * modifier;
        return 0;
      }).filter((row, index) => {
        let start = (this.currentPage-1)*this.pageSize;
        let end = this.currentPage*this.pageSize;
        if(index >= start && index < end) return true;
      });
    }
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