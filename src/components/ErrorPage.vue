<template>
    <div class="error-page">
        <div class="error-content">
            <p class="error-text">This product is unavailable to show</p>
            <button class="product-btn" @click="$emit('onNext')">
                Next Product
            </button>
        </div>
    </div>
</template>
<script>
export default {
    name: 'ErrorPage',
    // props: {
    //     isError: {
    //         type: Boolean,
    //         required: true
    //     }
    // }
}
</script>
<style>
.error-page {
    width: 100%;
    height: 100%;
    display: grid;
    place-items: center;
    position: relative;
}

.error-page::before {
    content: '';
    position: absolute;
    left: 10%;
    width: 90%;
    height: 90%;
    background: url('../assets/icons/sad-face.svg');
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
}

.error-content {
    z-index: 2;
}

.error-text {
    font-size: var(--font-md);
    margin-bottom: 13px;
    text-align: center;
}

.error-content button {
    margin: 0 auto;
    display: block;
    width: 100%;
    cursor: pointer;
}
</style>