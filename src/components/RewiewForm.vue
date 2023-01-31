<script>
app.component('rewiew-form', {

    template:
        // /*html*/
        '<form class="rewiew-form" @submit.prevent="onSubmit"><h3>Leave a rewiew</h3><label for="name">Name:</label><input id="name" v-model="name"><label for="rewiew">Rewiew:</label><textarea id="rewiew" v-model="rewiew"></textarea><label for="rating">Rating:</label><select id="rating" v-model.number="rating"><option>5</option><option>4</option><option>3</option><option>2</option><option>1</option></select><input class="button" type="submit" value="submit"></input></form>',
        data(){

            return{
                name: '',
                rewiew: '',
                rating: null
            }
        },
        methods: {
            onSubmit(){
                let productRewiew = {
                    name:this.name,
                    rewiew:this.rewiew,
                    rating:this.rating
                }
                this.$emit('rewiew-submitted', productRewiew)

                this.name= ''
                this.rewiew= ''
                this.rating= null
            }
        }
    

        
})
</script>