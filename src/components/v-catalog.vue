<template>
    <div class="v-catalog">
      <router-link :to="{name: 'cart', params:{cart_data: CART}}">
      <div class="v-catalog__link_to_cart">Cart: {{CART.length}}</div>
      </router-link>
      
        <h1>Catalog</h1>
        <div class="v-catalog__list">
            <v-catalog-item 
            v-for="product in PRODUCTS"
            :key="product.article"
            v-bind:product_data="product"
            @addToCart="addToCart"
            />
        </div>
        
    </div>
</template>

<script>
import vCatalogItem from './v-catalog-item.vue'
import {mapActions, mapGetters} from 'vuex'
export default {
    name: 'v-catalog',
  components: { vCatalogItem },
  props: {

  },
  data(){
      return {  
        
      }
  },
  computed: {
    ...mapGetters([
      "PRODUCTS",
      "CART"
    ])
  },
  methods: {
      addToCart(data){
          this.ADD_TO_CART(data)
      },
      ...mapActions([
        "GET_PRODUCTS_FROM_API",
        "ADD_TO_CART"
      ]),
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API()
    .then((response) => {
      if(response.data){
        console.log("Ответ с данными получен");
      }
    })
  }
    
}
</script>

<style lang="scss">
    .v-catalog{
        &__list{
             display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        align-items: center;
        }
        &__link_to_cart{
          position: absolute;
          top: 10px;
          right: 10px;
          padding: 16px;
          border: 1px solid #ccc;
          border-radius: 4px;
        }
       
    }
    
</style>