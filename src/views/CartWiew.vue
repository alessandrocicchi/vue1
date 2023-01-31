<script>
export default({
    props: {
        cart: {
            type: Number
        },
        color:{
            type: String 
        },
        blue: {
            type: Number
        },
        green: {
            type: Number
        },
        prizeBlue: {
            type: Number
        },
        prizeGreen: {
            type: Number
        }
    },
    data() {
        return{
            premium: true
        }
    },
    computed: {

        showCart() {
            return this.cart
        },
        showBlue() {
            return this.blue
        },
        showGreen() {
            return this.green
        },
        showPrizeBlue() {
            return this.prizeBlue
        },
        showPrizeGreen() {
            return this.prizeGreen
        },
        TotalBlue() {
            return this.showPrizeBlue*this.blue
        },
        TotalGreen() {
            return this.showPrizeGreen*this.green
        }
    }
})
</script>
<template>
<main>
    
    <div id="app">

<div class="nav-bar"></div>
<h2>Prova</h2>
<div class="cart">Number of products:{{ showCart }}</div>

<table class="tables">
    <tr>
        <th class="th">Product</th>
        <th class="th">Prize</th>
        <th class="th">Quantity</th>
        <th class="th">Total</th>
    </tr>
    <tr>
        <th class="th">Blue socks</th>
        <th class="th"> {{ showPrizeBlue }}</th>
        <th class="th">{{ showBlue }}</th>
        <th class="th">{{ TotalBlue }}</th>
    </tr>
    <tr>
        <th class="th">Green socks</th>
        <th class="th">{{ showPrizeGreen }}</th>
        <th class="th">{{ showGreen }}</th>
        <th class="th">{{ TotalGreen }}</th>
    </tr>
</table>

</div>
</main>
</template>
<style>

.th{
    border: 2px solid black;
    padding: 10px;
    
}
</style>