<template>
  <div id="app" :class="getClassByCategory(category)">
    <ProductDisplay @fetch-product="fetchProduct" :product="product" :filled-circles="filled" :is-error="error"/>
  </div>
</template>

<script>
import ProductDisplay from './components/ProductDisplay.vue'

export default {
  name: 'App',
  components: {
    ProductDisplay
  },
  data() {
    return {
      category: "men's clothing",
      product: null,
      counter: 0,
      filled: [],
      error: false
    }
  },
  methods: {
    getClassByCategory(category) {
      //Menentukan style berdasarkan class yang akan digunakan berdasarkan category
        if(category === "men's clothing") {
          return 'men'
        } else if(category === "women's clothing") {
          return 'women'
        } else {
          return ''
        }
    },
    async fetchProduct() {
        this.error = false
        if(this.counter === 20) {
          //Jika counter sudah mencapai 20, maka counter akan direset ke 1
            this.counter = 1
        } else {
          //Jika counter belum mencapai 20, maka counter akan ditambahkan 1
            this.counter++
        }
        
        try {
            //Mengambil data single product dari API berdasarkan counter
            const response = await fetch(`https://fakestoreapi.com/products/${this.counter}`)
            const data = await response.json()
            // Mengisi data product dengan data yang didapat dari API
            this.product = data
            // Mengisi data category dengan data yang didapat dari API
            this.category = data.category
            // Membulatkan rating ke atas -- Rating 3.9 berarti 4 lingkaran yang akan diisi
            const rating = Math.ceil(this.product.rating.rate)
            // Mengisi data filled dengan array yang berisi object yang berisi key filled dengan value false
            this.filled = new Array(5).fill({filled: false}).map((circle, index) => {
                if(index < rating) {
                    return {filled: true}
                } else {
                    return {filled: false}
                }
            })
        } catch(error) {
          // Jika terjadi error, maka error akan diisi true untuk menampilkan error page
            this.error = true
        }
    }
  },
  created() {
      //Mengambil data product pertama kali
      this.fetchProduct()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: grid;
  place-items: center;
  width: 100vw;
  height: 100vh;
  max-height: 100vh;
  position: relative;
}

#app::before, #app::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 60%;
}

#app::before {
  background-color: var(--secondary-color);
  z-index: -1;
}

#app::after {
  background: url('./assets/images/bg-pattern.png') no-repeat center top;
  z-index: -1;
}
</style>
