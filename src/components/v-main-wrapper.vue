<template>
    <div class="v-main-wrapper">
        <keep-alive>
          <router-view></router-view>     
        </keep-alive>
     
        <!-- <p>{{title}}</p>
        <v-catalog />
        <v-cart 
        v-if="CART.length"
        :cart_data="CART"
        /> -->

    </div>
</template>


<script>
// import VCart from './v-cart.vue';
// import VCatalog from './v-catalog.vue';
// import {mapGetters} from 'vuex'
export default {
    name: 'v-main-wrapper',
    // components: {
    //     VCatalog,
    //     VCart

    // },
     props: {

     },
     data(){
         return{
             title: ""
         }
     },
     computed: {
        //  ...mapGetters([
        //      "CART"
        //  ])
     },
     methods: {

     },
     watch: {

     },
     mounted(){
         console.log("Hello, I'm alive");
     }
    
}
</script>


<style scoped>
.v-main-wrapper{
    max-width: 900px;
    margin: 0 auto;
}
</style>