<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <h1>{{ title }}</h1>
  <ComponentTest1 hello-msg="ハローメッセージ" v-on:notification="handleEvent"/>
  <button @click="testMethod()">おためし</button>
  <hr class="double-line">
  <div class="bg-ghostwhite">
    <table>
      <tr>
        <th>1</th>
        <th>2</th>
        <th>3</th>
      </tr>
      <tr>
        <td>サンプル</td>
        <td>サンプル</td>
        <td>サンプル</td>
      </tr>
    </table>
  </div>
</template>

<script>
import ComponentTest1 from './components/ComponentTest1.vue'

export default {
  name: 'App',
  components: {
    ComponentTest1,
  },
  data: () => ({
    title: "ここにタイトル",
  }),
  methods: {
      testMethod() {
        return alert("HELLO!");
      },
      handleEvent() {
        return alert("子コンポーネントからの通知");
      },
  },
}
</script>

<style>
body {
  text-align: center;
}

.double-line {
  border-style: double;
}

.bg-ghostwhite {
  background-color: silver;
}

</style>
