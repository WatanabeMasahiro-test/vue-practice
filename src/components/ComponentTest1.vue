<template>
  <div class="hello">
    <p>{{ helloMsg }}</p>
    <button @click="$emit('notification')">通知</button>
    <hr>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    helloMsg: String
  },
  methods: {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
