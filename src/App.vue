<script setup lang="ts">
import { ref, onMounted } from 'vue'
import ComponentTest1 from './components/ComponentTest1.vue'
import axios from 'axios'

const title = 'ここにタイトル'
const bpi:any = ref(null)
const dbJson:any = ref(null)

const testMethod = () => alert('HELLO!')
const handleEvent = () => alert('子コンポーネントからの通知')

onMounted(() => {
  try {
    axios.get('https://api.coindesk.com/v1/bpi/currentprice.json')
      .then(function (response) {
        console.log(response.data.bpi) // デバッグ用にconsoleに出力
        bpi.value = response.data.bpi
      })
  } catch (error) {
    console.log(error)
    bpi.value = null
  }

  try {
    axios.get('/db.json')
      .then(function (response) {
        console.log(response.data.posts) // デバッグ用にconsoleに出力
        dbJson.value = response.data.posts
      })
  } catch (error) {
    console.log(error)
    dbJson.value = null
  }
})
</script>

<template>
  <div>
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
  </div>
</template>

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
