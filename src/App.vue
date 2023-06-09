<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <h1>{{ title }}</h1>
  <ComponentTest1 hello-msg="ハローメッセージ" @notification="handleEvent"/>
  <button @click="testMethod()">おためし</button>
  <hr class="double-line">
  <div class="bg-silver p-20px">
    <table v-if="bpi != false">
      <tr>
        <th></th>
        <th v-for="i in 5" :key="i">{{ i }}</th>
      </tr>
      <tr 
        v-for="(item, index) in bpi" 
        :key="item.id"
      >
        <th>{{ index }}</th>
        <td>{{ item.code }}</td>
        <td>{{ item.symbol }}</td>
        <td>{{ item.rate }}</td>
        <td>{{ item.description }}</td>
        <td>{{ item.rate_float }}</td>
      </tr>
    </table>

    <table v-if="dbJson != false">
      <tr>
        <th></th>
        <th v-for="i in 2" :key="i" class="w-100">{{ i }}</th>
      </tr>
      <tr
        v-for="(item) in dbJson" 
        :key="item.id"
      >
        <th>{{ item.id }}</th>
        <td>{{ item.title }}</td>
        <td>{{ item.score }}</td>
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
    margin: 20px auto;
    border: 1px solid;
    background-color: ghostwhite;
  }

  th, td {
    padding: 2px 10px
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

  .w-100 {
    width: 100px;
  }

</style>
