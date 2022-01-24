<template>
  <div>
    <button v-on:click="fetchData">click on me</button>
    <button v-on:click="toggleChart"> create</button>
    <MyChart :dataset="[this.covidData.map(row=>row.deaths)]" :labels="this.covidData.map(row => row.dateRep)"  v-if="isChart"/>
    <MyChart :dataset="[this.covidData.map(row=>row.popData2020)]" :labels="this.covidData.map(row => row.countriesAndTerritories)" v-if="isChart"/>
    <MyChart :dataset="[this.covidData.map(row=>row.popData2020), this.covidData.map(row=>row.deaths)]" :labels="this.covidData.map(row => row.countriesAndTerritories)" v-if="isChart"/>
  </div>

</template>

<script>
import MyChart from "./Chart";
export default {
  name: 'HelloWorld',
  components: {MyChart},
  data() {
   return{isChart: false,
   covidData: []
   }
  },
  methods: {
    fetchData() {
      fetch("COVID.csv").then(res => {
        return res.text()
      }).then(data => {
            let jsonObj = []
            let resultBody = data.split(/\r?\n|\r/)
            let headers = resultBody[0].split(',')
            for (let i = 1; i < resultBody.length; i++) {
              let dataObj = resultBody[i].split(',');
              let obj = {};
              for (let j = 0; j < dataObj.length; j++) {
                obj[headers[j].trim()] = dataObj[j].trim();
              }
              jsonObj.push(obj);
            }
        console.log(jsonObj)
        this.covidData = jsonObj
            return jsonObj
          }
      )
    },
    toggleChart(){
      this.isChart = true
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
