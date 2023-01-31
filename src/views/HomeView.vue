<script>
import { RouterView } from 'vue-router';
import CartWiew from './CartWiew.vue';
export default{
    data() {
        return {
            cart: 0,
            premium: true,            
            product: "Socks",
            brand: "Vue Mastery",
            selectedVariant: 0,
            details: ["50% cotton", "30% wool", "20% polyester"],
            variants: [
                { id: 2234, color: "green", image: "../public/socks_green.jpg", quantity: 50, prize: "4.99" },
                { id: 2235, color: "blue", image: "../public/socks_blue.jpg", quantity: 10, prize: "2.99" },
            ],
            blue: 0,
            green: 0,
            
        };
    },
    methods: {
        UpdateCart() {
            this.cart += 1;
            this.updateColor();
        },
        DowngradeCart() {
            this.cart -= 1;
            this.downgradeColor();
        }
        ,
        updateVariant(index) {
            this.selectedVariant = index;
        },
        updateColor() {
          
          if(this.selectedVariant == 0){
            this.green+=1;
          }else if(this.selectedVariant == 1){
            this.blue+=1;
          }
        },
        downgradeColor() {
          
          if(this.selectedVariant == 0){
            this.green-=1;
          }else if(this.selectedVariant == 1){
            this.blue-=1;
          }
        }
    },
    computed: {
        title() {
            return this.brand + " " + this.product;
        },
        image() {
            return this.variants[this.selectedVariant].image;
        },
        inStock() {
            return this.variants[this.selectedVariant].quantity;
        },
        shipping() {
            return this.variants[this.selectedVariant].prize;
        },
        cartWiew() {
            return this.cart;
        },
        blueQuantity() {
          return this.blue;
        },
        greenQuantity() {
          return this.green;
        },
        prizeColorBlue() {
            return 2.99
        },
        prizeColorGreen() {
            return 4.99
          }
    },
  components:{ RouterView, CartWiew }

}
</script>

<template>
  <main>
    <header>
      <div id="app">

      <div class="nav-bar"></div>
      <div class="cart" >Cart({{ cart }})</div>
        <RouterView />
        <div class="product-display">
        <div class="product-container">
            <div class="product-image">
                <img :src="image" class="images">
            </div>
            <div class="product-info">
                <h1 class="titles">{{title}}</h1>
                    <p v-if="inStock">In Stock</p>
                    <p v-else>Out of Stock</p>
                    <p>Shipping: {{ shipping }}</p>
                    <ul>
                        <li v-for="detail in details">{{ detail }}</li>
                    </ul>
                    <div v-for="(variant, index) in variants" :key="variant.id" @mouseover="updateVariant(index)" class="color-circle" :style="{ backgroundColor: variant.color }"></div>
                    <button class="add-button" :class="{ disabledButton : !inStock }" :disabled="!inStock" v-on:click="UpdateCart">Add To Cart</button>
                    <button class="remove-button" :class="{ disabledButton : !inStock }" :disabled="!inStock" v-on:click="DowngradeCart">Remove to Cart</button>
                    <CartWiew :cart="cartWiew" :blue="blueQuantity" :green="greenQuantity" :prize-blue="prizeColorBlue" :prize-green="prizeColorGreen" />
                  </div>
            </div>
    </div>
    </div>
    </header>
  </main>
</template>
<style>
.images {
width: 300px;
height: 350px;
}
.color-circle {
width: 50px;
height: 50px;
margin-top: 8px;
border: 2px solid #d8d8d8;
border-radius: 50%;
}
.add-button{

    height: 40px;
    width: 80px;
    background-color: darkcyan;
    color: white;
}
.remove-button{

height: 40px;
width: 80px;
background-color: red;
color: white;
}
</style>