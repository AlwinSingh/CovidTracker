<template>
  <div class="hello">
    <div class="alert">
  <span class="closebtn" onclick="this.parentElement.style.display='none';">&times;</span>
  Singaporeans advised to defer all non-essential travel abroad to reduce risk of contracting COVID-19 Infection
</div>
  </div>
</template>

<script>
export default {
  name: 'CovidAlert',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.alert {
  padding: 8px;
  background-color: #a10505; /* Red */
  color: white;
  font-size: 18px;
  letter-spacing: 1px;
  margin-bottom: 0px;
  border-bottom: 1px solid black;
}

/* The close button */
.closebtn {
  margin-left: 15px;
  color: white;
  font-weight: bold;
  float: right;
  font-size: 26px;
  line-height: 20px;
  cursor: pointer;
  transition: 0.3s;
}

/* When moving the mouse over the close button */
.closebtn:hover {
  color: black;
}
</style>
