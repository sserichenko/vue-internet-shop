<template>
    <div class="v-cart">
        <router-link :to="{name: 'catalog'}">
      <div class="v-catalog__link_to_cart">Back to catalog</div>
      </router-link>
        <h2>Cart</h2>
        <p v-if="!this.cart_data.length">There are no products in cart...</p>
        <v-cart-item 
        v-for="(item, index) in cart_data"
            :key="item.article"
            :cart_item_data="item"
            @deleteFromCart="deleteFromCart(index)"
            @increment="increment(index)"
            @decrement="decrement(index)"
        />
        <div class="v-cart__total">
            <p class="total__name">Total:</p>
            <p>{{cartTotalCost}} UAH</p>
        </div>
    </div>
</template>

<script>
import vCartItem from './v-cart-item.vue'
import {mapActions} from 'vuex'
export default {
    name: 'v-cart',
  components: { vCartItem },
  props: {
      cart_data: {
          type: Array,
          default: () => {
              return []
          }
      }
  },
  methods: {
      ...mapActions([
          "DELETE_FROM_CART",
          "INCREMENT_CART_ITEM",
            "DECREMENT_CART_ITEM"
      ]),
      deleteFromCart(index){
          this.DELETE_FROM_CART(index)
      },
      increment(index){
          this.INCREMENT_CART_ITEM(index);
      },
      decrement(index){
          this.DECREMENT_CART_ITEM(index);
      }
  },
  computed: {
      cartTotalCost(){
          if(this.cart_data.length){
              let result = [];
          for(let item of this.cart_data){
              result.push(item.price * item.quantity)
          }
          result = result.reduce(function(sum, el){
              return sum = sum + el
          })
          return result;
          }
          else{
              return 0
          }
          
      }
  }
    
}
</script>

<style lang="scss">
    .v-cart{
        padding: 40px 0px;
        &__total{
            position: fix;
            bottom: 0;
            left: 0;
            right: 0;
            padding: 8px 16px;
            display: flex;
            justify-content: center;
            background: #1c8d42;
            color: #fff;
            font-size: 22px;
            .total__name{
                margin-right: 20px;
                
            }
        }
    }
</style>