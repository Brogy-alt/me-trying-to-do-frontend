<template>
    <SpinnerComponent v-if="isSpinning" />
    <div v-else>
        <div class="card" style="width: 18rem;" v-for="product in products" :key="product.id">
            <img :src="product.imgURL" class="card-img-top" alt="...">
            <div class="card-body">
                <h5 class="card-title">{{ product.prodName }}</h5>
                <p class="card-text">{{ product.prodGenre }}</p>
                <p class="card-text">{{ product.price }}</p>
                <a href="#" class="btn btn-primary">Go somewhere</a>
            </div>
        </div>
    </div>
</template>

<script>
import SpinnerComponent from '@/components/SpinnerComponent.vue';

export default {
    components: {
        SpinnerComponent
    },
    computed: {
        products() {
            return this.$store.state.products;
        }
    },
    mounted() {
        this.$store.dispatch('fetchProducts')
    },
    created() {
        setTimeout(() => {
            this.isSpinning = false;
        }, 3000);
    },
    data() {
        return {
            isSpinning: true
        }
    }
}
</script>