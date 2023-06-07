<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <h1>{{ title }}</h1>
  <ComponentTest1 hello-msg="ハローメッセージ" :notification="handleEvent"/>
  <button @click="testMethod()">おためし</button>
  <hr class="double-line">
  <div class="bg-silver p-20px">
    <table v-if="bpi != false">
      <tr>
        <th>1</th>
        <th>2</th>
        <th>3</th>
      </tr>
      <tr>
        <td v-for="item in bpi" :key="item.id">{{ item.code }}</td>
      </tr>
      <tr>
        <td v-for="item in bpi" :key="item.id">{{ item.symbol }}</td>
      </tr>
      <tr>
        <td v-for="item in bpi" :key="item.id">{{ item.rate }}</td>
      </tr>
      <tr>
        <td v-for="item in bpi" :key="item.id">{{ item.description }}</td>
      </tr>
      <tr>
        <td v-for="item in bpi" :key="item.id">{{ item.rate_float }}</td>
      </tr>
    </table>

    <table v-if="dbJson != false">
      <tr>
        <th>1</th>
        <th>2</th>
        <th>3</th>
        <th>4</th>
        <th>5</th>
        <th>6</th>
      </tr>
      <tr>
        <td v-for="item in dbJson" :key="item.id">{{ item.title }}</td>
      </tr>
      <tr>
        <td v-for="item in dbJson" :key="item.id">{{ item.score }}</td>
      </tr>
      <tr>
        <td v-for="item in dbJson" :key="item.id">{{ item.id }}</td>
      </tr>
    </table>

  </div>
</template>

<script>
import ComponentTest1 from './components/ComponentTest1.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    ComponentTest1,
  },
  data: () => ({
    title : "ここにタイトル",
    bpi   : null,
    dbJson: null, 
  }),
  methods: {
      testMethod() {
        return alert("HELLO!");
      },
      handleEvent() {
        return alert("子コンポーネントからの通知");
      },
  },
  mounted: function(){
    axios.get('https://api.coindesk.com/v1/bpi/currentprice.json')
      .then(function(response){
        // console.log(response.data.bpi)  // デバッグ用にconsoleに出力
        this.bpi = response.data.bpi;
      }.bind(this))
      .catch(function(error){
        console.log(error);
        this.bpi = false;
      }
    );
    axios.get("/db.json")
      .then(function(response){
        // console.log(response.data.posts)  // デバッグ用にconsoleに出力
        this.dbJson = response.data.posts;
      }.bind(this))
      .catch(function(error){
        console.log(error);
        this.dbJson = false;
      }
    );
  },
}
</script>

<style>
body {
  text-align: center;
}

table, td, th {
  margin: auto;
  border: 1px solid;
  background-color: ghostwhite;
}

.double-line {
  border-style: double;
}

.bg-silver {
  background-color: silver;
}

.p-20px {
  padding: 20px;
}

</style>
