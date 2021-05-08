<template>

<!-- <form>
  <label>
    Choose your preferred party date (required, April 1st to 20th):
    <input dateControl.value = '2017/06/01' v-model="date" type="date" name="party" min="2017/4/20" max="2027/4/20" required>
    <span class="validity"></span>
  </label>

  <p>
    <button>Submit</button>
  </p>
</form> -->

<p>Pick a date</p>
 <div class="bg-white shadow rounded px-3 pt-3 pb-5 border border-white">
    <div >
      <div >  
      
        <col cols="12" sm="12">     
          <input
          v-model="year"
          placeholder ="Year"
          :min = "2018"
          :max = "2021"
          type="number"
          class="mt-1 block w-full border-gray p-1"/>
        </col>
      
      </div>
      <br>
      <div>
        <input
        v-model="month"
         placeholder ="Month"
         :min = "1"
         :max = "12"
          type="number"
          month="month"
       class="mt-1 block w-full border-gray p-1"/>
      </div><br>
      <div>
       
        <input
        v-model="day"
         placeholder ="Day"
         :min = "1"
         :max = "31"
          type="number"
          day="day"
          class="mt-1 block w-full border-gray p-1"/>
    </div>
    <br>

    <div class=" mt-5">
      <div class="col text-right">
        <button @click="dateFormat()"
          class="bg-green-400 px-4 py-2 rounded" >
          Add date
        </button>
      </div>
    </div>
  </div>


<div v-if ="items"> 
<div v-for="(item, index) in items">
<div>
<h3>
<a v-bind:href="item.content_urls.desktop.page">{{ index + 1  }}. {{ item.titles.normalized }} </a>
</h3>
</div>
<div>
{{ item.description }}
</div >
<div v-if ="item.thumbnail">
 <img :src="item.thumbnail.source"/>
</div>
</div>
   
  </li>
  
  </div>
  
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
    data () {
    return {
      loading: true,
      errored: false,
       items:[],
       thumbnail:[],
      year: null,
      month: null,
      day: null,
      date: null,
    }
      },
  
  props: {
    msg: String
  },
 
  methods:{
dateFormat() {
    let day = this.day;
    let month = this.month;
    let year = this.year;
    let link = this.link;

    let date = year + "/" + month + "/" + day
    if (month < 10) {
          date = year + "/0" + month + "/" + day
    }
    if (day < 10) {
          date = year + "/" + month + "/0" + day
    }
    if (month < 10 && day < 10) {
          date = year + "/0" + month + "/0" + day
    }
    this.date = date
    axios
  
      .get("https://en.wikipedia.org/api/rest_v1/feed/featured/" + date)
      .then(response => {
        this.items = response.data.mostread.articles
        this.thumbnail = response.data.mostread.articles.thumbnail
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
      }
    },
  
mounted () {
    axios
  
      .get('https://en.wikipedia.org/api/rest_v1/feed/featured/2021/04/30')
      .then(response => {
        this.items = response.data.mostread.articles
        this.thumbnail = response.data.mostread.articles.thumbnail
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
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
.border-gray {
  border-bottom: 1px solid rgba(55, 65, 81, 0.3);
  border-radius: 0;
}
</style>
