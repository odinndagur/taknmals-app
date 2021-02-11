<template>
  <div class="sign-card">
    <div class="centered" v-if="!selected" :class="{ isSelected: selected }">
    <a @click="$emit('select')" :class="{ isSelected: selected }">{{sign.phrase}}</a>
    </div>


    <div class="centered" v-if="selected" :class="{ isSelected: selected }">
    <a @click="$emit('select')" :class="{ isSelected: selected }">{{sign.phrase}}</a> <br/>

        <div class="player">
      <youtube
        v-if="selected"
        :video-id="sign.youtubeId"
        :fitParent="true"
      ></youtube>
    </div>

<div class="list">
<ul>
  <li v-for="word in sign.related" :key="word">
{{word}}
  </li>
</ul>
</div>
    </div>


  </div>
</template>

<script>
export default {
  name: "SignCard",
  props: {
    sign: {},
    selected: Boolean,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.list {
  margin:auto;
  vertical-align: middle;
}
.sign-card {
  width:80%;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  /* display: inline-block; */
  margin: 10px 10px;
}
a {
  color: #gray;
}
a:hover{
  cursor: pointer;
}
.isSelected {
  color: red;
}

/* @media screen and (max-width: 600px) {
  .player {
    width: 400px;
    margin: auto;
  }
} */

.player {
  width:80%;
  max-width: 450px;
  float:left;
  margin: auto;
}
</style>
