<template>
  <ProductDetail />
</template>

<script>
import ProductDetail from "./product-detail/ProductDetail.vue";
export default {
  name: "N11 Ürün Detay",
  components: {
    ProductDetail
  },
  props: {
    msg: String,
  },
  mounted() {
    document.title = "N11 Ürün Detay";
  },
};
</script>

