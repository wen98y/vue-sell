<template>
  <div class="cartcontrol">
    <div class="cart-decrease" v-show="food.count>0" @click.stop.prevent="decreaseCart" transition="move">
      <span class="inner icon-remove_circle_outline"></span>
    </div>
    <div class="cart-count" v-show="food.count>0">{{ food.count }}</div>
    <div class="cart-add icon-add_circle" @click.stop.prevent="addCart"></div>
  </div>
</template>

<script>
import Vue from 'vue';

export default {
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    addCart(event) {
      if (!event._constructed) {
        return;
      }
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1);
      } else {
        this.food.count++;
      }
      this.$dispatch('cart.add', event.target);
    },
    decreaseCart(event) {
      if (!event._constructed) {
        return;
      }
      this.food.count--;
    }
  }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
.cartcontrol
  font-size: 0
  .cart-decrease
    display: inline-block
    padding: 6px
    transition: all .4s linear
    // 这里把2个动画 translate rotate 一起写了
    &.move-transition
      opacity: 1
      transform: translate3d(0, 0, 0)
      .inner
        // 设为inline-block才有高度，否则高度为0，不能做动画
        display: inline-block
        font-size: 24px
        line-height: 24px
        color: rgb(0, 160, 220)
        transform: rotate(0deg)
        transition: all .4s linear
    &.move-enter, &.move-leave
      opacity: 0
      transform: translate3d(24px, 0, 0)
      .inner
        display: inline-block
        font-size: 24px
        line-height: 24px
        color: rgb(0, 160, 220)
        transform: rotate(180deg)
        transition: all .4s linear
  .cart-count
    display: inline-block
    vertical-align: top
    width: 12px
    padding-top: 6px
    line-height: 24px
    text-align: center
    font-size: 10px
    color: rgb(147, 153, 159)
  .cart-add
    display: inline-block
    font-size: 24px
    padding: 6px
    line-height: 24px
    color: rgb(0, 160, 220)
</style>
