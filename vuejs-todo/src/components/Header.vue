<template>
  <header>
    <h1>{{greating}}</h1>
    <h2>{{message}}</h2>
    <span>{{ hours }}:{{ minutes }}:{{ seconds }}</span>
  </header>
</template>

<script>

export default {
  data() {
    return {
      greating: 'Welcome',
      message: 'It is time to be productive!'
    }
  },

  props: ['hours', 'minutes', 'seconds']
}

</script>

<style scoped>
header {
  background-color: #6FA198;
  margin-top: 20px;
  margin-bottom: 8px;
  padding-top: 20px;
  padding-bottom: 20px;
  border-radius: 25px;
  text-align: center;
}

span {
  font-size: 30px;
}
</style>
