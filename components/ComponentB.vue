<template>
  <div style="background-color: chocolate">
    <slot />
    <div v-if="dataRef" class="scroll-container">
      <div class="scroll-content">
        <div class="product-card" v-for="product in dataRef" :key="product.id">
          <img :src="product.image" alt="Product Image" style="height: 300px" />
          <h3>{{ product.title }}</h3>
          <p>${{ product.price }}</p>
        </div>
      </div>
    </div>
    <div v-else>loading...</div>
  </div>
</template>
<script setup>
const dataRef = ref(undefined);
onMounted(async () => {
  const { data, pending, error, refresh } = await useFetch(
    "https://fakestoreapi.com/products?limit=5"
  );
  dataRef.value = data.value;
  console.log(data);
});
</script>
<style>
.scroll-container {
  overflow-x: auto;
}

.scroll-content {
  display: flex;
  flex-wrap: nowrap;
}

.product-card {
  flex: 0 0 auto;
  width: 300px;
  margin-right: 20px;
  /* 其他樣式設定 */
}
</style>
