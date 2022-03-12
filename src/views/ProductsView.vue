<template>
  <h2>產品列表</h2>
  <div class="container">
    <div class="row row-cols-1 row-cols-lg-4 g-3">
      <div class="col" v-for="product in products" :key="product.id">
        <div class="card h-100">
          <!-- <img :src="product.imageUrl" class="card-img-top" alt="..." /> -->
          <div :style="{backgroundImage: `url(${product.imageUrl})`}"
          style="height: 200px; background-size:cover; background-position: center center"></div>
          <div class="card-body">
            <h5 class="card-title">{{ product.title}}</h5>
            <p class="card-text" style="height: 4.5rem; overflow:hidden">
              {{ product.description}}
            </p>
            <router-link :to="`/product/${product.id}`" class="btn btn-primary">產品資料</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      products: []
    }
  },
  methods: {
    getProducts () {
      this.$http(
        `${process.env.VUE_APP_API}/api/${process.env.VUE_APP_PATH}/products/all`
      ).then((res) => {
        this.products = res.data.products
      })
    }
  },
  mounted () {
    this.getProducts()
  }
}
</script>
