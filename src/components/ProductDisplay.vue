<script>
export default{
    name: "productDisplay",
    props: {
        premium: {
            type: Boolean,
            required: true
        },
    },
    data() {
        return {
            product: "Socks",
            brand: "Vue Mastery",
            selectedVariant: 0,
            details: ["50% cotton", "30% wool", "20% polyester"],
            variants: [
                { id: 2234, color: "green", image: "../public/socks_green.jpg", quantity: 50, prize: "4.99" },
                { id: 2235, color: "blue", image: "../public/socks_blue.jpg", quantity: 10, prize: "2.99" },
            ],
            rewiews: []
        };
    },
    methods: {
        addToCart() {
            this.$emit("add-to-cart");
        },
        removeToCart() {
            this.$emit("remove-to-cart");
        },
        updateVariant(index) {
            this.selectedVariant = index;
        },
        addRewiew(rewiew) {
            this.rewiews.push(rewiew);
        },        
        
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
        }
    }
}
</script>
<template>
    <body>
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
                    <button class="add-button" :class="{ disabledButton : !inStock }" :disabled="!inStock" v-on:click="addToCart">Add To Cart</button>
                    <button class="remove-button" :class="{ disabledButton : !inStock }" :disabled="!inStock" v-on:click="removeToCart">Remove to Cart</button>
                    <button class="link-button" ><RouterLink to="/MyCart">My Cart</RouterLink></button>
                </div>
            </div>
    </div>
</body>
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
.link-button{
height: 40px;
width: 80px;
background-color: white;
color: chartreuse;
}
</style>