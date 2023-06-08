<template>
    <h1>Product lists</h1>
  <div class="row pb-3">
    <div
      class="col-lg-3 col-sm-6"
      v-for="product in products"
      :key="product.id"
    >
      <div class="row p-2">
        <div class="col-12 p-1">
          <div class="card border-0 p-3 shadow border-top border-5 rounded">
            <img :src="product.images[0]" class="card-img-top rounded" style="height: 280px; width: 90%" />

            <div class="card-body pb-0">
              <div class="pl-1">
                <p
                  class="card-title h5 text-dark opacity-75 text-uppercase text-center"
                >
                  {{ product.title }}
                </p>
                <p class="card-title text-info text-center">
                  by <b>{{ product.brand }}</b>
                </p>
              </div>
              <div class="pl-1">
                <p class="text-dark opacity-75 text-center m-b-0">
                  <b> Price:</b>
                  <span class=""> {{ product.price }}</span>
                </p>
                <p class="text-dark opacity-75 text-center">
                    <b>Category:</b>
                  <span class="">
                   {{product.category}}
                  </span>
                </p>
                <p  class="text-dark opacity-75 text-center">
                    <b>Stock:</b>
                  <span class="">
                   {{product.stock}}
                  </span>
                </p>
              </div>
            </div>
            <div>
              <router-link :to="{name: 'productDetails', params: { id: product.id }}" class="btn btn-primary bg-gradient border-0 form-control">
                Details
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const products = ref([]);
    const errorMessage = ref(null);
    try {
      const fetchData = async () => {
        const data = await fetch("http://localhost:3000/products");
        if (!data.ok) {
          throw Error("No Product Available");
        }
        console.log(data);
        products.value = await data.json();
      };
      fetchData()
    } catch (err) {
      errorMessage.value = err.message;
    }
    
    return { products };
  },
};
</script>

<style>
</style>