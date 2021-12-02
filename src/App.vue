<template>
  <div id="app">
<div class="searchBox">
<input v-model="search"/>
</div>
<br/>
<div v-for="sign in currentArr" :key="sign.youtubeId" :class="{selected: isSelected(sign)}">
    <SignCard class="sign-card2" :sign="sign" @select="select(sign)" :selected="isSelected(sign)"/> 
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
      for(let i = 0; i < 40; i++){
        this.currentArr.push(this.takn[i]);
      }
    },
    loadMore(){
      let initial = this.currentArr.length;
      for(let i = initial; i < initial + 10; i++){
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
filteredList(){
  return this.takn.filter(takn => takn.phrase.toLowerCase().includes(this.search.toLowerCase());
  },
},
  },
  mounted(){
    this.getInitial();
    this.scroll();
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.sign-card {
  display:inline-block;
  /* margin:auto; */
  width:30px;
}
.selected{
/* margin:20px; */
}

div {
}
</style>
