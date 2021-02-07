<template>
  <tr class="item">
    <td class="image">
        <img class="itemImage" :src="product.image">
    </td>
    <td>{{product.name}}</td>
    <td class="price">{{product.price | number_format}}円（税込）</td>
    <td class="componentTd">
      <input type="number" id="productCount" class="count number" v-model.number="count" min="0" step="1"/>
      <input ref="productId" type="hidden" id="productId" :value="product.id"/>
    </td>
    <td class="componentTd">
      <button class="cartButton" @click="clickAdd">追加</button>
    </td>
  </tr>
</template>

<script>
import './filter.js';

export default {
  name: 'product',
  props: ['product'],
  data: function() {
    return {
      // 購入個数
      count: 0
    }
  },
  methods: {
    // 「追加」ボタンが押下されたとき親コンポーネントのaddCartメソッドを呼び出す
    clickAdd: function() {
      var id = this.$refs.productId.value;
      this.$emit('addCart',id,this.count)
    }
  }
}
</script>

<style>
td.image {
	width: 72px;
}

img.itemImage {
	width: 70px;
	height: 70px;
}

.componentTd {
	text-align: center;
}

.number {
	text-align: right;
}

.count {
	width: 50px;
}
</style>