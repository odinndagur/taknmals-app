<template>
  <div id="app">
<div class="searchBox">
<input class="search-box" v-model="search"/>
</div>
<br/>
<div class="signslist">
<div v-for="sign in currentArr" :key="sign.youtubeId" :class="{selected: isSelected(sign)}">
    <SignCard class="sign-card2" :sign="sign" @select="select(sign)" :selected="isSelected(sign)"/> 
</div>
</div>
<!-- <br/> -->
<button @click="loadMore">Add more signs</button>
  </div>
</template>

<script>
import taknjson from "./assets/takn.json";
import SignCard from './components/SignCard'
export default {
  name: "App",
  components:{
    SignCard,
  },
  data: () => {
    return {
      takn: taknjson,
      currentArr: [],
      selected: {},
      search:'',
    };
  },
  methods: {
    getInitial(){
      for(let i = 0; i < 150; i++){
        this.currentArr.push(this.takn[i]);
      }
    },
    loadMore(){
      let initial = this.currentArr.length;
      for(let i = initial; i < initial + 50; i++){
        this.currentArr.push(this.takn[i]);
      }
    },
    select(sign){
      console.log(sign.phrase)
      if(this.selected == sign){
        this.selected = {};
      }
      else{
        this.selected = sign;
      }
    },
    isSelected(sign){
      return this.selected == sign;
    },
    scroll () {
  window.onscroll = () => {
    let bottomOfWindow = Math.max(window.pageYOffset, document.documentElement.scrollTop, document.body.scrollTop) + window.innerHeight === document.documentElement.offsetHeight

    if (bottomOfWindow) {
      this.loadMore();
        }
 }
}
  },
  computed: {
    // filteredList(){
    //   if (this.takn[0].phrase){
    //   return this.takn.filter(item=> item.phrase.toLowerCase().indexOf(this.search) != -1);
    //   }
    //   else return this.takn;
    // }
// filteredList(){
//   return this.takn.filter(takn => takn.phrase.toLowerCase().includes(this.search.toLowerCase());
//   }
},
  mounted(){
    this.getInitial();
    this.scroll();
  }
};
</script>

<style>
html, body {
    max-width: 100%;
    overflow-x: hidden;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}

.search-box{
  width:80%;
  margin:0 10%;
}
.searchBox{
  position: sticky;
  top: 0px;
  padding: 10px 0px;
}

.signslist {
  height:80%;
  overflow-y:auto;
  top:30px;
}
.sign-card {
  display:inline-block;
  /* margin:auto; */
  width:30px;
  padding:0 4rem;
  margin-top: 0.2rem;
  margin-bottom: 0.2rem;
  background:white;
  border-radius:1%;
  box-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;
}
.selected{
/* margin:20px; */
margin-top:1rem;
padding-top:1rem;
border-top: 2px solid gray;
margin-bottom:1rem;
padding-bottom:1rem;
border-bottom:2px solid gray;
}

div {
}
</style>
