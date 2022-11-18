<template>
  <div id="app">
    <div id="app" class="my-5 flex-container">
      <div class="sidenav">
        Sort By
        <ul>
          <li>
            
          </li>
          </ul>
      </div>
      <div class="content">
        <h1>My online store</h1>
        <div class="container mx-auto mt-4">

      
        <div class="d-flex flex-wrap w-100 justify-content-between">
          <div class=" me-1 card" v-for="(product, index) in listOfProduct">
            <div class="card-body card-h">
              <!-- <h5 class="card-title">{{ product.name }}</h5> -->
              <img src="./assets/Your-Life-in-Pictures-Cover.jpg" class="card-img-top" alt="..." />
              <div class="mt-2 card-body-content d-flex flex-column justify-content-between">
                <div class="mt-2 ">
                  <h6 class="card-subtitle mb-2 text-muted">Name: {{ product.name }}</h6>
                  <h6 class="card-subtitle mb-2 text-muted">Location: {{ product.location }}</h6>
                  <h6 class="card-subtitle mb-2 text-muted">Price: {{ product.price }} </h6>
                  <h6 class="card-subtitle mb-2 text-muted">Spaces : {{ product.spaces }}</h6>
                </div>
                <div>
                  <button class="btn btn-primary" :disabled=isBtn @click="addToCart(product, index)">Add to cart
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
        <h3 class="mt-3">Shopping Cart</h3>
        <div class="d-flex flex-wrap w-100 justify-content-between">
          <div class=" me-1 card" v-for="(product, index) in selectedProduct">
            <div class="card-body" v-if="product.isVisible">
              <img src="./assets/Your-Life-in-Pictures-Cover.jpg" class="card-img-top" alt="..." />
              <div class="mt-2 d-flex flex-column justify-content-between">
                <div>
                  <h6 class="card-subtitle mb-2 text-muted">Name: {{ product.name }}</h6>
                  <h6 class="card-subtitle mb-2 text-muted">Location: {{ product.location }}</h6>
                  <h6 class="card-subtitle mb-2 text-muted">Price: £{{ product.price }} </h6>
                  <h6 class="card-subtitle mb-2 text-muted">Spaces : {{ product.spaces }}</h6>
                </div>
                <div>
                  <button class="btn btn-primary" :disabled=isBtn @click="removeFromCart(product, index)">Remove from
                    cart
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
        <h3>Checkout</h3>
        <form class="mt-3">
          Name: <input type="text" v-model="form.name" class="form-group" placeholder="Name">
          Phone: <input type="number" v-model="form.number" class="form-group" placeholder="Phone">
          <button class="btn btn-primary">Checkout</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import { ProductList } from "./lessons";

export default {
  name: 'app',
  data() {
    return {
      avalaibleProducts: 5,
      isBtn: false,
      listOfProduct: [],
      selectedProduct: [],
      toShowSelectedProduct: [],
      form: {
        name: "",
        number: ""
      }
    }
  },
  validations: {
    // form: {
    //   name: { required },
    //   number: { required }
    // }
  },
  created() {

    this.listOfProduct = ProductList
  },
  methods: {
    addToCart(product, index) {

      if (product.spaces > 0 && this.selectedProduct) {
        product.spaces--;
        const addToCartproduct = this.selectedProduct.find(x => x.id == product.id);
        if (addToCartproduct) {
          this.selectedProduct.forEach(x => {
            if (x.id == product.id) {
              x.spaces++;
            }
          });
        } else {
          const firstProduct = {
            id: product.id,
            name: product.name,
            location: product.location,
            price: product.price,
            spaces: 1,
            isVisible: true
          }
          this.selectedProduct.push(firstProduct);
        }
      } else {
        console.log('out of stock')
      }
    },
    removeFromCart(product, cart) {
      if (product.spaces == 0) {
        this.selectedProduct.splice(cart, 1)
      }
      if (product.spaces > 0 && this.listOfProduct) {
        product.spaces--;
        const addToCartproduct = this.listOfProduct.find(x => x.id == product.id);
        if (addToCartproduct) {
          this.listOfProduct.forEach(x => {
            if (x.id == product.id) {
              x.spaces++;
            }
          });
        } else {
          const firstProduct = {
            id: product.id,
            name: product.name,
            location: product.location,
            price: product.price,
            spaces: 1,
            isVisible: true
          }
          this.listOfProduct.push(firstProduct);
        }
        if (product.spaces == 0) {
          this.selectedProduct.splice(cart, 1)
        }
      }
    }
  }
}
</script>

<style>
html, body{
    margin: 0 !important;
    padding: 0 !important;
    width: 100%;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.flex-container {
  display: -webkit-flex;
  display: flex;
  background-color: red;
  min-height: 100%;
}

.sidenav {
  background-color: lightgray;
  -webkit-flex: 1;
  flex: 1;
}
.content {
  background-color: rgb(248, 253, 255);
  padding: 10px;
  -webkit-flex: 5;
  flex: 5;
  height: 2000px;
}


.card {
  max-height: 380px;
  height: 380px;
  width: 200px;
  margin: 5px 5px;
}

.card-body-content {
  height: 180px;
}

.card-body {
  padding: 0.50rem;
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
