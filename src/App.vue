<template>
  <div id="app">
    <div id="app" class="container my-5">
      <h1>My online store</h1>

      <div class="card" style="width: 18rem;">
        <div class="card-body">
          <h5 class="card-title">Product</h5>
          <img src="./assets/Your-Life-in-Pictures-Cover.jpg" class="card-img-top" alt="..."/>
          <div class="mt-2">
            <h6 class="card-subtitle mb-2 text-muted">Subject : Maths</h6>
            <h6 class="card-subtitle mb-2 text-muted">Location : London</h6>
            <h6 class="card-subtitle mb-2 text-muted">Price : £100</h6>
            <h6 class="card-subtitle mb-2 text-muted">Spaces : {{ avalaibleProducts }}</h6>
            <button class="btn btn-primary" :disabled=isBtn @click="addToCart()">Add to cart </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      avalaibleProducts: 5,
      isBtn:false
    }
  },
  methods: {
    addToCart() {
      if (this.avalaibleProducts) {
        this.avalaibleProducts--
      }
      else{
        console.log("no product left")
        this.isBtn=true 
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
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
</style>
