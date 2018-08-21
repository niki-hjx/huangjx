<template>
  <div class="hello">
   
    <h2 class="news">新闻列表
      <div class='random' @click='getrandom'>换一换</div>
    </h2>
    <div v-once>{{getnews()}}</div>
    <ul>
    <li v-for='(v,i) in msg' :class='{current:i==cur}' @click='cur=i'> 
        {{v.title}}
      </li>
    </ul>
    <div class='right'>
      <h2>{{msg[cur].title}}</h2>
      <img :src="msg[cur].image" alt="">
      <p>{{msg[cur].content}}</p>
      <span>{{msg[cur].update}}</span>
    </div>
   
  </div>
</template>

<script>
export default {
  name: 'detail',
  data () {
    return {
      msg: [0],  //给一个初始值，还没开始读的时候就先编写
      cur:0
    }
  },
  methods:{
    getnews(){
      var url='/api';
      this.$axios.get(url)
      .then(response=>{
      // console.log(response)
        this.msg=response.data;
      })
      .catch(error=>{
        console.log(error);
      })
    },
    getrandom(){
      var url='/api';
      this.$axios.post(url,{   //get服务器不支持参数，所以用post
        params:{
          pageIndex:2    /*Math.floor(Math.random()*20+1)*/
        }
      })
      .then(response=>{
      // console.log(response)
        this.msg=response.data;
        this.cur=0;
      })
      .catch(error=>{
        console.log(error);
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
.news{
  height: 50px;
}
.random{
    width: 90px;
    float: right;
    background: #c00;
    border-radius: 21px;
}
ul {
  width: 31%;
  list-style-type: none;
  padding: 0;
  /* display:flex; */
  flex-wrap:wrap;
  position: absolute;
  border: 1px solid #ccc;
  box-shadow: 2px 2px 2px 2px;
}
li {
  width:100%;
  height: 90px;
  overflow:hidden;
  /* margin: 10px 0; */
  border-bottom: 1px solid #000;
  flex-wrap:wrap;
}
.right{
  width: 68%;
  float: right;
  height: 455px;
  border: 1px solid #ccc;
  margin-top: 17px;
  background: #999;
  box-shadow: 2px 2px 2px 2px;

}
.right img{
  float: left;
    margin-top: 100px;
    width: 40%;
}
.right p{
    float: right;
    width: 57%;
    margin-top: 100px;
    /* text-align: center; */
    text-align: left;
}
.current{
  background: #c00;
}
a {
  color: #42b983;
}
</style>
