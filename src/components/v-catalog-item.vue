<template>
    <div class="v-catalog-item">
        <img :src=" require('../assets/images/' + product_data.image) " class="v-catalog-item__image" alt="img">
        <p class="v-catalog-item__name">{{product_data.name}}</p>
        <p class="v-catalog-item__price">Price: {{product_data.price}} UAH</p>
        <button 
        class="v-catalog-item__add_to_cart_button btn"
        @click="addToCart"
        >Add to Cart
        </button>
    </div>
</template>

<script>
export default {
    name: 'v-catalog-item',
    props:{
        product_data: {
            type: Object,
            default: () => {}
        }
    },
    data() {
        return {
            
        }
    },
    computed: {

    },
    methods: {
        addToCart(){
            this.$emit("addToCart",this.product_data)
        }
    },
        mounted(){
        this.$set(this.product_data, "quantity", 1)
    }
}
</script>

<style lang="scss">
    .v-catalog-item{
        flex-basis: 25%;
        box-shadow: 0 0 8px 0 #e0e0e0;
        padding: 16px;
        margin-bottom: 16px;
        &__image{
            width: 100px;
        }
    }
</style>
    
