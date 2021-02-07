<template>
  <div class="condition">
    <label for="category">カテゴリー</label>
    <select id="category" class="categorize"
      :value="selectedCategory" 
      @change="$emit('categoryChanged',parseInt($event.target.value));">
      <option>▼選択してください</option>
      <option 
        v-for="category in categories" 
        :value="category.id" 
        :key="category.id">
        {{category.name}}
      </option>
    </select>
    <label for="search">商品名（部分一致）</label>
    <input type="text" v-model="keyword">
    <button @click="clickSearch">検索</button>
  </div>
</template>

<script>
export default {
  name: 'productHeader',
  props: ['selectedCategory','categories'],
  data: function() {
    return {
      keyword: ''
    }
  },
  methods: {
    // 「検索」ボタンが押下されたとき親コンポーネントのsearchProductメソッドを呼び出す
    clickSearch: function() {
      this.$emit('searchProduct',this.keyword)
    }
  }
}
</script>

<style>
.condition {
	width: 680px;
  margin: 0 auto;
  margin-top: 30px;
}

.condition select{
  margin-right: 30px;
}

.condition input {
  margin-right: 5px;
} 
</style>