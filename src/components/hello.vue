<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button>click</button>   
  </div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'Welcome to component A !'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1{
	color: #22B089;
	font-size: 20px;
	font-weight: bold;
}
</style>
