<template>
  <v-container>
    <v-row>
      <v-col v-for="product in products" :key="product.id" cols="12" md="4" sm="6">
        <v-card height="100%">
          <v-img height="20rem" :src="product.images[0]" />
          <v-card-title>{{ product.title }}</v-card-title>
          <v-card-subtitle>${{ product.price }}</v-card-subtitle>
          <v-card-text>{{ product.description }}</v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import Vue from "vue";
import { TProduct } from "@/utils/models/product";

export default Vue.extend({
  data: () => ({
    products: [] as TProduct[],
  }),

  created() {
    const fetchProducts = async () => {
      const products = await fetch("https://dummyjson.com/products")
        .then((res) => res.json())
        .then<TProduct[]>((res) => res.products);

      this.products = products;
    };

    try {
      fetchProducts();
    } catch (error) {
      console.log(error);
    }
  },
});
</script>
