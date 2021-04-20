<template>
  <main class="grey lighten-5 pa-2">     
    <section> 
      <h2 class="display-1">Our active projects</h2>
      <v-row align="center" justify="center">  
        <stat-card 
          v-for="card in cards" 
          :key="card.title"
          :cardTitle="card.title"
          :bgColor="card.bgColor"
          :cardAmount="card.amount"
          :cardAmountNew="card.amountNew"
          :cardIcon="card.icon"
          />
      </v-row>
    </section> 
    <section> 
      <h2 class="display-1">Visuals</h2>  
      <v-row align="center" justify="center"> 
        <line-chart
          v-for="visual in visuals"
          :key="visual.id"
          :chart-data="visual.chartData"
          :options="visual.option" 
          class="ma-1" 
        >
        </line-chart>      
      </v-row>
    </section>
  </main>
</template>

<script>
import StatCard from './StatCard'
import LineChart from './LineChart'

  export default {
      name: 'Total',     
      data: () => ({
        cards: [
            {
              title: 'total cases',
              bgColor: 'primary lighten-2',
              amount: 0,
              amountNew: 0,
              icon: 'mdi-alert-box'
            },
            {
              title: 'deaths',
              bgColor: 'red accent-2',
              amount: 0,
              amountNew: 0,
              icon: 'mdi-emoticon-dead'
            },
            {
              title: 'recoveries',
              bgColor: 'tel lighten-1',
              amount: 0,
              amountNew: 0,
              icon: 'mdi-hospital-box'
            },
          ],
        
        visuals: [{  
          id: 1,
          chartdata: null,
          options: {
            responsive: true,
            maintainAspectRatio: false
          }
        }], 
        continents: null,
        allData: null,
      }),    
      components: {
        StatCard, LineChart
      },
      mounted () {
        this.axios
          .get('https://corona.lmao.ninja/v2/continents?sort')
          .then(response => { this.continents = response; this.updateStats() })
          .catch(error => {console.error("An API error:", error)})

        this.axios
          .get('https://corona.lmao.ninja/v2/historical/all')
          .then(response => { this.allData = response; this.updateVisuals() })
          .catch(error => {console.error("An API error:", error)})  
      },
      methods: {
        updateStats () {
          let data = this.continents.data
          let cases = 0
          let todayCases = 0
          let deaths = 0
          let todayDeaths = 0
          let recovered = 0

          for (let elem of data) {
            cases += elem.cases
            todayCases += elem.todayCases
            deaths += elem.deaths
            todayDeaths += elem.todayDeaths
            recovered += elem.recovered
          }
          this.cards[0].amount += cases         
          this.cards[0].amountNew += todayCases   
          this.cards[1].amount += deaths
          this.cards[1].amountNew += todayDeaths  
          this.cards[2].amount += recovered
        },
/*        updateVisuals () {
          let data = this.allData.data.recoveriesPerDay
          let labels = []
          let casesPerDay = []          

       
          this.visuals.push (
            {              
                id: 1,
                chartData: {
                  labels: [],
                  datasets: [
                    {
                      label: 'Total cases',
                      backgroundColor: '#26a69a',
                      data: recoveriesPerDay
                    }
                  ]
                },
                options: {
                  responsive: true,
                  maintainAspectRatio: false
                }
            },         
            {
              id: 2,
              chartData: {
                labels: [],
                datasets: [
                  {
                    label: 'recoveries',
                    backgroundColor: '#26a69a',
                    data: recoveriesPerDay
                  }
                ]
              },
              options: {
                responsive: true,
                maintainAspectRatio: false
              }
            },
            {
              id: 3,
              chartData: {
                labels: [],
                datasets: [
                  {
                    label: 'recovered',
                    backgroundColor: '#26a69a',
                    data: recoveriesPerDay
                  }
                ]
              },
              options: {
                responsive: true,
                maintainAspectRatio: false
              }
            }
          )

          let lastDayCases = casesPerDay[casesPerDay.length - 1] - casesPerDay[casesPerDay.length - 2]

          this.cards[0].amountNew += lastDayCases
          this.cards[1].amountNew += parseInt(deathsPerDay[deathsPerDay.length - 1])
          this.cards[2].amountNew += parseInt(recoveredPerDay[recoveredPerDay.length - 1])
        }
  */    }
  }
</script>
<style>
  .small {
    width: 100%;
    height: 100%;
    max-width: 600px;
    margin: auto;
  }
</style>
