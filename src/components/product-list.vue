<template>
  <div class="container">
    <product-header
      :selectedCategory="selectedCategory"
      :categories="categories"
      :keyword="keyword"
      @categoryChanged="categoryChanged"
      @searchProduct="searchProduct"
    >
    </product-header>
    <div class="noResult" v-if="filteredList.length == 0">検索結果がありません。</div>
    <table class="top" v-if="filteredList.length > 0">
      <tr>
      <th>画像</th><th>商品名</th><th>価格(円)</th><th>個数</th><th>カート</th>
      </tr>
      <product
      v-for="product in filteredList" 
      :product="product" 
      :key="product.id"
      @addCart="addCart"
      >
      </product>
    </table>
  </div>
</template>

<script>
import productHeader from './product-header.vue';
import product from './product.vue';

export default {
  name: 'productList',
  props: ['products'],
  components: {
    'product-header': productHeader,
    'product': product
  },
  data: function() {
    return {
      //「カテゴリー」の選択状態
      selectedCategory: 0,
      // 「カテゴリー」の選択値
      categories: [
          {id: 1, name: '犬'},
          {id: 2, name: '猫'},
          {id: 3, name: 'モルモット'},
          ],
      // 検索ワード
      keyword: '',
    }
  },
  methods: {
    // 「カテゴリー」の選択値が変わったとき呼び出されるメソッド
    categoryChanged: function(select) {
      // 現在の選択値を新しい選択値で上書きする
      this.selectedCategory = select;
    },
    // 「検索」ボタンが押下されたとき呼び出されるメソッド
    searchProduct: function(keyword) {
      // 現在の値を新しい値で上書きする
      this.keyword = keyword;
    },
    // 「追加」ボタンが押下されたとき呼び出されるメソッド
    addCart: function(id, count) {
      var productId = id;
      var productCount = count;
      // 購入個数が0の場合の処理
      if (productCount == 0) {
          alert("個数が0です。");
          return ;	
      }
      // カート画面へリダイレクト
      location.replace(`/sampleweb/cart/add?productId=${productId}&productCount=${productCount}`);
    }
  },
  computed: {
    // 絞り込み後の商品リストを返す算出プロパティ
    filteredList: function() {
      // 絞り込み後の商品リストを格納する新しい配列
      var newList = [];
      for (var i=0; i<this.products.length; i++) {
        // 表示対象かどうかを判定するフラグ
        var isShow = true;
        // i番目の商品が表示対象かどうかを判定する
        if (this.selectedCategory==1 && this.products[i].category!=1) {
            isShow = false; // この商品は表示しない
        } else if (this.selectedCategory==2 && this.products[i].category!=2) {
            isShow = false; // この商品は表示しない
        } else if (this.selectedCategory==3 && this.products[i].category!=3) {
            isShow = false; // この商品は表示しない
        }
        if (this.products[i].name.indexOf(this.keyword) == -1) {
            isShow = false; // この商品は表示しない
        }
        // 表示対象の商品だけを新しい配列に追加する
        if (isShow) {
          newList.push(this.products[i]);
        }
      }
      // 絞り込み後の商品リストを返す
      return newList;
    }
  }
}
</script>

<style>
div.container {
	border-radius: 20px;
	width: 70%;
	min-width: 680px;
	background: #ffffff;
	margin: 20px auto;
	padding: 5px;
	text-align: center;
}

table {
	width: 680px;
	margin: 10px auto;
}

th {
	padding: 5px;
	height: 20px;
	vertical-align: middle;
	background: #a3d6cc;
	border: 1px solid #6c3524;
	font-weight: normal;
}

.top th {
	border-bottom: 5px solid #6c3524;
}

td {
	vertical-align: middle;
	padding: 3px;
	border: 1px solid #a3d6cc;
}

.noResult {
  color: #FF0000;
  margin: 30px;
}
</style>