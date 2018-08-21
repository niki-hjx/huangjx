<template>
  <div class="hello">
   
    <h2>Essential Links</h2>
    <button @click='getnews'>获得新闻信息</button>
    <button @click='getmore'>获得更多新闻</button>
    <ul>
        <li v-for='v in msg'>
          <img :src='v.image'>
          {{v.title}}
        </li>
    </ul>
    <span v-for='i in 10' @click='getmore(i)'>
      {{i}}
    </span>
    
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: []
    }
  },
  methods:{
    getnews(){
      var url='/api';
      this.$axios.get(url)
      .then(response=>{
      console.log(response)
        this.msg=response.data;
      })
      .catch(error=>{
        console.log(error);
      })
    },
    getmore(index=1){
      var url='/api';
      this.$axios.post(url, {
        pageSize:12,
        pageIndex:index
  })
  .then(response=> {
    console.log(response);
    this.msg=response.data;
  })
  .catch(function (error) {
    console.log(error);
  });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
  display:flex;
  flex-wrap:wrap;
}
li {
  width:25%;
  height: 300px;
  overflow:hidden;
  margin:10px;
}
a {
  color: #42b983;
}
</style>
