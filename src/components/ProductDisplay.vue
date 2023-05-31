<template>
    <div class="product-display-wrapper">
        <ErrorPage v-if="isError" @onNext="$emit('fetch-product')"/>
        <div class="content" v-else>
            <div v-if="product" class="product flex-align-center" :id="`${product.title}-${product.id}`">
                <div class="product-image flex-align-center">
                    <img :src="product.image" :alt="product.title">
                </div>

                <div class="product-details">
                    <h1 class="product-title">{{ product.title }}</h1>
                    <div class="product-category-rating">
                        <p class="product-category">{{ product.category }}</p>
                        <div class="rating-circles flex-align-center">
                            <div class="rating">{{ `${product.rating.rate}/${circles}` }}</div>
                            <div class="circles">
                                <span v-for="(circle, i) in filledCircles" :key="i" class="circle" :class="{filled: circle.filled}"></span>
                            </div>
                        </div>
                    </div>
                    <p class="product-desc">
                        {{ product.description }}
                    </p>

                    <h1 class="product-price">
                        {{ `$${product.price}` }}
                    </h1>

                    <div class="product-actions">
                        <button class="product-btn buy-btn">Buy Now</button>
                        <button class="product-btn next-btn" @click="$emit('fetch-product')">Next Product</button>
                    </div>
                </div>
            </div>

            <div v-else>
                <LoadingComponent />
            </div>
        </div>
    </div>
</template>
<script>
import LoadingComponent from "./LoadingComponent.vue";
import ErrorPage from "./ErrorPage.vue";

export default {
    components: { LoadingComponent, ErrorPage },
    //Mengirimkan event emit ke parent
    emits: ["fetch-product"],
    props: {
        //Berisi data product yang dikirimkan dari parent
        product: {
            type: Object,
            default: null
        },
        // Berisi data filledCircles yang dikirimkan dari parent untuk menentukan jumlah lingkaran yang akan diisi
        filledCircles: {
            type: Array,
            required: true
        },
        // Berisi data isError yang dikirimkan dari parent untuk menentukan apakah terjadi error atau tidak
        isError: {
            type: Boolean,
            required: true,
            default: true
        }
    },
    data() {
        return {
            // Jumlah lingkaran yang dapat diisi
            circles: 5
        };
    },
}
</script>
<style>
.product-display-wrapper {
    width: 80%;
    min-height: 80%;
    height: fit-content;
    padding: 1rem;
    background: #FFFFFF;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
    border-radius: 10px;
    display: grid;
    place-items: center;
}

.content {
    width: 100%;
}

.product-image, .product-image img, .product-details {
    width: 50%;
}

.product-image img {
    object-fit: cover;
}

.product-details {
    padding: 0 1rem;
}

.product-details h1 {
    font-size: var(--font-lg);
    color: var(--primary-color);
}

.product-category, .rating {
    color: var(--secondary-text-color);
}

.product-category-rating {
    display: flex;
    justify-content: space-between;
    margin-top: 1rem;
    font-size: var(--font-sm);
}

/* Memberi jarak pada setiap circles */
.rating-circles {
    gap: 1rem;
}

/** Membuat lingkaran */
.circle {
  display: inline-block;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  border: 1px solid var(--primary-color);
  margin-right: 5px;
}

.filled {
  background-color: var(--primary-color);
}

.product-desc {
    margin: 1rem 0;
    padding: 1rem 0;
    border: 1px solid #00000033;
    border-right: none;
    border-left: none;
    font-size: var(--font-md);
}

.product-actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 1rem;
    margin-top: 1rem;
}

.buy-btn {
    background: var(--primary-color);
    color: #FFFFFF;
    border: none;
}

.next-btn {
    background: #FFFFFF;
    border: 3px solid var(--primary-color);
    color: var(--primary-color);
}

.next-btn:hover {
    background: var(--primary-color);
    color: #FFFFFF;
}

/* Membuat responsive */

@media screen and (max-width: 768px) {
    .product-image, .product-details {
        width: 100%;
        margin: 10px 0;
    }

    .product-image img {
        width: 50%;
    }

    .product, .product-actions {
        flex-direction: column;
    }
}
</style>