<template>
  <div id="app">
    <div class="searchBox">
      <input class="search-box" @keydown="updateSearch" v-model="search"/>
      <div class="btncenter">
        <button @click="loadMore">Add more signs</button>
        </div>
      <div class="btncenter">
        <button @click="getAll">Get all signs</button>
      </div>
    </div>
    <br/>
    <div class="signslist">
      <div v-for="sign in filteredList" :key="sign.youtubeId" :class="{selected: isSelected(sign)}">
          <SignCard class="sign-card" :sign="sign" @select="select(sign)" :selected="isSelected(sign)"/> 
      </div>
    </div>
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
      currentArr: [
        {'phrase': '',
        'youtubeId': '',

        }
      ],
      filteredArr: [],
      selected: {},
      search:'',
    };
  },
  methods: {
    getInitial(){
      for(let i = 0; i < 150; i++){
        this.currentArr.push(this.takn[i]);
      }
      //this.filteredArr = this.currentArr;
    },
    loadMore(){
      let initial = this.currentArr.length;
      for(let i = initial; i < initial + 50; i++){
        this.currentArr.push(this.takn[i]);
      }
    },
    getAll(){
      while(this.currentArr.length < this.takn.length-50){
        this.loadMore();
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
    updateSearch(){
      this.filteredArr = this.currentArr.filter(item=>{
        console.log(item['phrase'])
        item['phrase'].indexOf(this.search) != -1;
})
      console.log("lol")
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
        filteredList() {
          if(this.takn != null){
              if(this.search != ''){
              return this.currentArr.filter(sign => {
                return sign['phrase'].toLowerCase().includes(this.search.toLowerCase())
              })
            }
          }
            return this.currentArr;
        },
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
    overflow: hidden;
    height:100%;
    margin:0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top:60px;
  height:100vh;
  width:100vw;
}

.search-box{
  width:80%;
  margin:auto 10%;
}
.searchBox{
  margin:auto auto;
  /* padding: 10px 0px; */
  position:sticky;
  top:0;
}

.btncenter{
margin:10px auto;
width:fit-content;
}

.signslist {
  height:100%;
  overflow-y:auto;
  overflow-x: hidden;
  max-width:80%;
  margin:auto;
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
</style>
