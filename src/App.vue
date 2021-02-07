<template>
  <div id="app">
    <product-list :products="products"></product-list>
  </div>
</template>

<script>
import productList from './components/product-list.vue'

export default {
  name: 'App',
  components: {
    'product-list': productList
  },
    data: function() {
      return {
        // 商品リスト
        products: [
            { id: 1, name: '柴犬（赤）', price: 200000, image: require('./assets/images/dog001.jpg'), category: 1},
            { id: 2, name: '柴犬（黒）', price: 250000, image: require('./assets/images/dog002.jpg'), category: 1},
            { id: 3, name: '柴犬（白）', price: 150000, image: require('./assets/images/dog003.jpg'), category: 1},
            { id: 4, name: '猫（ハチワレ）', price: 10000, image: require('./assets/images/cat001.jpg'), category: 2},
            { id: 5, name: '猫（茶トラ）', price: 10000, image: require('./assets/images/cat002.jpg'), category: 2},
            { id: 6, name: '猫（三毛）', price:10000, image: require('./assets/images/cat003.jpg'), category: 2},          
            { id: 7, name: 'モルモット（ショート）', price: 5000, image: require('./assets/images/mol001.jpg'), category: 3},
            { id: 8, name: 'モルモット（アビシニアン）', price:5000, image: require('./assets/images/mol002.jpg'), category: 3},
            { id: 9, name: 'モルモット（テディ）', price:5000, image: require('./assets/images/mol003.jpg'), category: 3}
        ]
      }
  }
}
</script>

<style>
body {
	background: linear-gradient(#a3d6cc, #ffffff) fixed;
}
</style>
