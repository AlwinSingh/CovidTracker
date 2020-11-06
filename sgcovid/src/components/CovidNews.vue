<template>
  <div class="hello">
    <h3 class="pb-3 text-dark mr-5 pr-5">Channel News Asia Latest COVID Updates</h3>
    
    <div class="covidnewsholder">

    <div class="card" id="covid-box3" style="width: 50rem; height: auto;">
      <div class="card-body">
    <h5 class="card-title pb-4">COVID-19 Deaths</h5>
    <h6 class="card-subtitle text-muted" style="font-size: 17px;" id="covidnews"><strong>Retrieving Articles...</strong></h6>
    <br>
      </div>
    </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'CovidNews',
}

var postHtml = "";

function fetchNews() {
var count = 0;
postHtml = "";
//document.getElementById('covidnews').innerHTML = "";
fetch("http://newsapi.org/v2/top-headlines?country=sg&apiKey=703b5c8c9834431d915e571fd3415443", {
        "method": "GET",
    })
    .then(response => response.json()) // Getting the actual response data
    .then(data => {
      for (var i = 0; i < data.articles.length; i++) {
      if (data.articles[i].author == "CNA") {
        var stringsearch = (data.articles[i].title).toLowerCase().search("covid");
        if (stringsearch != -1) {
          count++;
          postHtml += "<a class='text-dark' target=_blank href='"+data.articles[i].url+ "'>" + count + ". " +data.articles[i].title + "<br><br>";
        }
       }
      }
      if (postHtml.length < 1) {
       document.getElementById('covidnews').outerHTML = "The API has no recent news available";
      } else {
       document.getElementById('covidnews').outerHTML= postHtml;
      }
    })
    .catch(err => {
        console.log(err);
    });
}

  setInterval(fetchNews, 1000);
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #covidnews {
    text-align: left;
    width: 100%;
    color: #1a1a1a;
    font-size: 20px;
  }
</style>
