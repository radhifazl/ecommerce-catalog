<template>
    <div class="flex-align-center">
        <div class="bar" v-for="bar in 3" :key="bar"></div>
    </div>
</template>
<script>
export default {
    name: 'LoadingComponent'
}
</script>
<style>
.bar {
    width: 30px;
    height: 20px;
    background-color: var(--secondary-color);
    margin: 0 10px;
    border-radius: 5px;
    animation: loading 1s infinite;
}

@keyframes loading {
    0% {
        height: 20px;
    }
    50% {
        height: 40px;
        background: var(--primary-color);
    }
    100% {
        height: 20px;
    }
}
</style>