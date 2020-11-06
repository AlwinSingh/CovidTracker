<template>
  <div id="app">
    <CovidAlert/>
    <div id="web-banner">
          <img class="covidlogo mb-4" alt="Virus logo" src="./assets/covidlogo.png"><br>
          <button v-b-modal.modal-dorscon class="btn btn-danger text-light">What is Dorscon?</button>
          <button class="btn btn-danger text-light mx-5">What is COVID-19?</button>
          <button class="btn btn-danger text-light">How can i stay safe?</button>
          <button class="btn btn-danger text-light ml-5">What are the symptoms?</button>
    </div>
    <HelloWorld/>
    <br>

    <h3 id="currentTime" class="pt-4 text-dark" style="font-size: 23px;"><p style="color: black;">{{currentTime}}</p>Retrieving Time..</h3>

    <div class="row pt-3">
<div class="col-3 mx-auto d-block">
    <table class="table nationaltable">
  <thead class="thead-dark border border-dark">
    <tr>
      <th scope="col">Carbohydrates</th>
      <th scope="col">Proteins</th>
      <th scope="col">Vegetables</th>
    </tr>
  </thead>
  <tbody class="border border-dark text-dark">
    <tr>
      <td><strong> 3 Months</strong></td>
      <td><strong>> 2 Months</strong></td>
      <td><strong>> 2 Months</strong></td>
    </tr>
  </tbody>
</table>
</div>
</div>

    <h3 class="pt-2 text-dark" style="font-size: 20px;font-family: 'arial';"><strong>Dorscon Level: <p style="font-size: 20px;color: #eb8807;">{{dorsconLevel}}</p></strong></h3>
    
    <!-- <pie-chart class="piechart ml-auto pt-5" :legend="false" :data="chartData" :colors="['#3c43c7', '#9467f5', '#760985', '#0f81a3']" width="470px" height="470px"></pie-chart> -->
    
    <div class="container mx-auto d-block" style="margin-top: 100px;">
    <div class="card" id="covid-box" style="width: 30rem; height: 12.5rem;">
      <div class="card-body">
    <h5 class="card-title pb-4">COVID-19 Cases</h5>
    <h6 class="card-subtitle text-muted"><strong  id="covidcases">Retrieving Cases...</strong></h6>
    <h6 class="card-subtitle text-muted pt-4"><strong>Imported: 86</strong></h6>
    <br>
    <p class="text-danger"><strong>13 Cases are Critical</strong></p>
      </div>
    </div>

    <br>

    <div class="card" id="covid-box2" style="width: 30rem; height: 7.5rem;">
      <div class="card-body">
    <h5 class="card-title pb-4">COVID-19 Recovered Cases</h5>
    <h6 class="card-subtitle text-muted"><strong id="covidrecovered">Retrieving Recovered Cases...</strong></h6>
    <br>
      </div>
    </div>

    <br>

    <div class="card" id="covid-box3" style="width: 30rem; height: 7.5rem;">
      <div class="card-body">
    <h5 class="card-title pb-4">COVID-19 Deaths</h5>
    <h6 class="card-subtitle text-muted"><strong id="coviddeaths">Retrieving Death Cases...</strong></h6>
    <br>
      </div>
    </div>
    </div>


  <b-modal id="modal-dorscon" title="What is Dorscon?">
    <p class="my-4">
      <img class="px-1" src="https://www.gov.sg/-/media/gov/ncov/dorsconlevel.jpg" alt="DorsconLevels" style="width: 465px;height: 400px;">


      When there is an outbreak resulting in the spread of an infectious disease worldwide, Singapore puts in place prevention and response plans.
      <br><br>
      As part of this plan, the ‘Disease Outbreak Response System Condition’ (DORSCON) is a colour-coded framework that shows the current disease situation. The framework provides us with general guidelines on what needs to be done to prevent and reduce the impact of infections.
      <br><br>
      DORSCON takes into account:
      <br>
      The current disease situation overseas<br>
      How transmissible the disease is<br>
      How likely it is to arrive in Singapore<br>
      What impact it may have on Singapore’s community

      <br><br>
      There are 4 statuses – Green, Yellow, Orange and Red, depending on the severity and spread of the disease. For each status, it details the impact on the community, such as the measures to be taken in daily life (e.g. temperature screening, border measures), and advice to the public (e.g to look out for travel advisories).
      <br><br>
      During the SARS experience in Singapore, the status was Orange, meaning the disease was severe and spread easily, but still contained.

      </p>
  </b-modal>

  <br><br><br><br><br><br>
  <CovidNews/>
  <br><br><br><br><br><br>
  <customfooter />
    </div>

</template>

<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.7.1/Chart.min.js"></script>
<script src="https://unpkg.com/vue-chartjs/dist/vue-chartjs.min.js"></script>

<script>
import HelloWorld from './components/HelloWorld.vue'
import CovidDetails from './components/CovidDetails.vue'
import CovidAlert from './components/CovidAlert.vue'
import CovidNews from './components/CovidNews.vue'
import customfooter from './components/sitefooter.vue'


//COVID-19 ENDPOINT
var localcases = 2;
var importedcases = 2;
var criticalcases = 2;
var recoveredcases = 2;

function fetchData() {
fetch("https://covid-19-coronavirus-statistics.p.rapidapi.com/v1/stats?country=Singapore", {
        "method": "GET",
        "headers": {
"x-rapidapi-host": "covid-19-coronavirus-statistics.p.rapidapi.com",
"x-rapidapi-key": "a956020b36mshbc989587cdbca3dp1be327jsnb4fd2dca34d4"
        }
    })
    .then(response => response.json()) // Getting the actual response data
    .then(data => {      
        // var sqlTime = (data.data.covid19Stats[0].lastUpdate).split("T");
        // console.log(sqlTime.join(", "));
        localcases += data.data.covid19Stats[0].confirmed;
        document.getElementById("covidcases").innerText = "Total: " +data.data.covid19Stats[0].confirmed;
        recoveredcases += data.data.covid19Stats[0].recovered
        document.getElementById("covidrecovered").innerHTML = "Recovered Cases: " +data.data.covid19Stats[0].recovered;
        document.getElementById("coviddeaths").innerHTML = "Deaths: " +data.data.covid19Stats[0].deaths;
    })
    .catch(err => {
        console.log(err);
    }); 
}

var testcase = document.getElementById("covidcases")

setInterval(fetchData, 1000);

var days = new Array("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday");
var months = new Array("January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December");
var date, time;

function getTime() {
var suffix = "AM";
var today = new Date();
date = days[today.getDay()] + ", " + today.getDate() + " " + months[(today.getMonth()+1)-1] + " " + today.getFullYear();

var seconds = today.getSeconds();

if (today.getHours() >= 12) {
  suffix = "PM";
} else if (today.getHours() >= 0 && today.getHours() < 12) {
  suffix = "AM";
}



time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds() + " " + suffix;

document.getElementById("currentTime").innerHTML = date + " | " + time;
}

setInterval(getTime, 1000);

export default {
  name: 'App',
  components: {
    HelloWorld,
    CovidDetails,
    CovidAlert,
    CovidNews,
    customfooter
  },
  data() {
    return {
      chartData: {
        'Local Cases' : localcases,
        'Imported Cases' : importedcases,
        'Critical Cases' : criticalcases,
        'Recovered Cases' : recoveredcases
      },
      dorsconLevel: 'Orange',
      currentTime: date,
      localCases: localcases,
      importedCases: importedcases,
      criticalCases: criticalcases,
      recoveredCases: recoveredcases
    }
  }
}
</script>

<style>
p {
  display: inline;
}

body {
 background-color: #f6f9fc !important;
}

#web-banner {
  height: 400px;
  width: 100%;
  background: linear-gradient(-90deg,#000000,#1f1e1e) !important;
  border-bottom: 1px solid black;
  box-shadow: 0px 3px 20px rgba(0, 0, 0, 0.93) ,1px 2px 2px rgba(0,0,0,.31) , -1px -2px 2px rgba(0,0,0,.15) ;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.covidlogo {
  height: 300px;
  width: 300px;
  margin-top: 4px;
}

.piechart {
  margin-right: 250px;
}

#covid-box {
  color: #525252;
  text-align: left;
  font-size: 15px;
  margin: 0 auto;
  float: none;
}


#covid-box2 {
  color: #027dbf;
  text-align: left;
  font-size: 15px;
  margin: 0 auto;
  float: none;
}

#covid-box3 {
  color: #b00505;
  text-align: left;
  font-size: 15px;
  margin: 0 auto;
  float: none;
}

</style>
