<template>
  <div class="hello">
    <div id="imglogo">
      <img class="logoPokemon" src="../assets/Pokemon.jpeg" alt="#">
    </div>
    <input id="namepoke" type="text" class="form-control" v-on:change="changepk">
    <p>{{this.namepk}}</p>
    <h1 id="idh1">Trouve ton POKEMON</h1>
    <button v-on:click="clicked">clicked</button>
    <button v-on:click="hide">hide</button>
    <button v-on:click="show">show</button>
    
       <!-- <p>{{this.reqpoke}}</p> -->
  <ul id="v-for-object" class="demo">
    <li class="nomPoke" v-for="value in this.reqpoke">
    {{ value.name }}
    </li>
  </ul>
  </div>
</template>

<script>


import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      info: null,
      reqpoke:null,
      namepk:null
    
    }
  }
  ,
  methods: {
    clicked: function () {
      console.log("click")
    },
    hide: function () {
      console.log("hide")
      document.getElementById("idh1").style.display = 'none';
    },
    show: function () {
      console.log("show")
      document.getElementById("idh1").style.display = 'block';
    },
    create: function () {

    },
    changepk(event){
      var url="https://pokeapi.co/api/v2/pokemon/"+document.getElementById("namepoke").value
      axios
      .get(url)
      .then(response =>{
        this.namepk = response.data.name
      console.log(response)})
    }
  },
  mounted () {
    axios
      .get('https://pokeapi.co/api/v2/pokemon/?offset=0&limit=200')
      .then(response =>{
        this.reqpoke = response.data.results
      console.log(response)})
  },
  
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
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#v-for-object{
  display: flex;
  flex-direction: column;
}

#idh1{
  font-family: "Comic Sans MS", cursive, sans-serif;
  size: 24px;
  color: #42b983;
  font-weight: bold;
}

.logoPokemon{
  width: 300px;
  height: 250px;
}

#imglogo{
  width: 100%;
  height: 300px;
  display: flex;
  justify-content: center;
}

.nomPoke{
  font-weight: bold;
  font-size: 14px;
 font-family: "Comic Sans MS", cursive, sans-serif;
  color: #424874;
  
}

</style>
