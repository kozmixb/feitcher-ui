<template>
  <div class="container">
    <div class="row">
      <div class="col p-4 d-flex flex-wrap justify-content-between">
        <Products
          v-for="(value, key) in products"
          :key="key"
          :id="key"
          :title="value"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Products from "./components/Product.vue";

export default {
  components: { Products },
  data() {
    return {
      products: {},
    };
  },
  created() {
    this.fetchProducts();
  },
  computed: {
    product_url: function () {
      return `${process.env.VUE_APP_API_URL}/api/products`;
    },
  },
  methods: {
    fetchProducts: function () {
      axios.get(this.product_url).then((res) => {
        this.products = res.data.products;
        console.log("Products loaded");
      });
    },
  },
};
</script>