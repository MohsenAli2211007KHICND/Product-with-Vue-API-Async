<template>
    <h1>Product's Details</h1>
    <form >
        <div class="card shadow border-0 mt-4 mb-4">
            <div class="card-header bg-secondary bg-gradient text-dark py-4">
                <div class="row">
                    <div class="col-12 text-center">
                        <h3 class="text-white text-uppercase">{{ product.title }}</h3>
                        <p class="text-white-50 fw-semibold mb-0">{{ product.brand }}</p>
                    </div>
                </div>
            </div>
            <div>
                <router-link to="/products"
                    class="btn btn-outline-warning bg-gradient mb-5 fw-semibold btn-sm text-uppercase">
                    <small>Back to home</small>
                </router-link>
            </div>
            <div class="card-body pb-0">
                <div v-for="image in product.images" :key="image">
                    <img :src="image" class="card-img-top rounded" style="height: 280px; width: 50%" />
                </div>
                <div class="pl-1">
                    <p class="card-title h5 text-dark opacity-75 text-uppercase text-center">
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
                            {{ product.category }}
                        </span>
                    </p>
                    <p class="text-dark opacity-75 text-center">
                        <b>Stock:</b>
                        <span class="">
                            {{ product.stock }}
                        </span>
                    </p>
                    <p class="text-dark opacity-75 text-center">
                        <b>Description:</b><br>
                        <span class="">
                            {{ product.description }}
                        </span>
                    </p>
                    <p class="text-dark opacity-75 text-center">
                        <b>Discount:</b>
                        <span class="">
                            {{ product.discountPercentage }}
                        </span>
                    </p>
                    <p class="text-dark opacity-75 text-center">
                        <b>Rating:</b>
                        <span class="">
                            {{ product.rating }}
                        </span>
                    </p>
                </div>
                <div class="row">
                    <div class="col-md-12 pb-1">
                        <a  @click="handleSubmit" class="btn btn-primary bg-gradient  w-100 py-2 text-uppercase fw-semibold">
                            Add to Cart
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </form>
</template>

<script>
import { ref } from "vue";
import { useRouter } from 'vue-router';
export default {
    props: ["id"],
    setup(props) {
       
            const router = useRouter();
            console.log(router);
        const product = ref([]);
        try {
            const fetchData = async () => {
                const data = await fetch(`http://localhost:3000/products/${props.id}`);
                if (!data.ok) {
                    throw Error("No Product Available");
                }
                console.log(data);
                product.value = await data.json();
            };
            fetchData();
        } catch (err) {
            console.log(err.message);
        }
        function handleSubmit(){
            router.push({name: 'products'})
        }

        return { product, handleSubmit};
    },
};
</script>

<style></style>