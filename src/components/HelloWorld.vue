<template>
  <div class="hello">
    <img src="https://www.logolynx.com/images/logolynx/f8/f8e7f0189842f58b3116214bf0fc173c.png" />
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  methods: {
  },
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

div{
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

img{
  max-width: 10%;
  padding: 20px;
  align-items: center;
  justify-content: center;
}

h3 {
  margin: 40px 0 0;
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
</style>
