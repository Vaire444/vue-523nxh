<template>
<div v-if ="items"> 
<div v-for="(item, index) in items">
<div>
<h3>
<a v-bind:href="item.content_urls.desktop.page">{{ index + 1  }}. {{ item.titles.normalized }} </a>
</h3>
</div>
<div>
{{ item.description }}
</div>
<div>
 <img :src="item.thumbnail"/>
</div>
</div>
<!-- 

  <li v-for="item in items" :key="item">
   {{ items.mostread }} -->
    <!-- {{ items.displaytitle }}  -->
<!-- {{ items.description }} -->
    <!-- {{ items.tfa.mostread}} -->
    
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
      //  year: 2021,
      //  month: 04,
      //  day: 29
    }
    
  },
  props: {
    msg: String
  },
mounted () {
    axios
      .get('https://en.wikipedia.org/api/rest_v1/feed/featured/2021/04/30')
      .then(response => {
        console.log (response.data)
        this.items = response.data.mostread.articles
         this.thumbnail = response.data.mostread.articles.thumbnail
         console.log("olen siin")
         console.log(this.thumbnail)
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
</style>
