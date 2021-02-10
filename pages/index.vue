<template>
  <div class="container">
    <Gallery :products="products" />
  </div>
</template>

<script>
// import axios from 'axios'
export default {
  data () {
    return {
      products: this.products
    }
  },
  fetch () {
    this.getToken().then((res) => {
      console.log(res)
      this.token = res
      this.getProducts().then((res) => {
        this.products = res
      })
    })
  },
  mounted () {
    const data = this
    window.onscroll = function (ev) {
      if ((window.innerHeight + window.scrollY) >= document.body.offsetHeight) {
        data.getProducts(0, data.products.length + 10).then((res) => {
          data.products = res
        })
      }
    }
  },
  methods: {
    async getToken () {
      const headers = {
        Authorization: 'Basic QlphYS1hdjVMNlJtWktsUGdaYUdOa2VhOmpjaGJmX1E1elJXQ2FFZzRUQ0I0bTljTElpb1BpbWww'
      }
      const tokenRes = await this.$axios.post('https://auth.commercetools.co/oauth/token?grant_type=client_credentials&scope=view_products:nuts-custom-demo-1', {},
        { headers })
      return tokenRes.data.access_token
    },
    async getProducts (offset = 0, limit = 10) {
      const headers = {
        Authorization: 'Bearer ' + this.token
      }
      const productRes = await this.$axios.get('https://api.commercetools.co/nuts-custom-demo-1/products', { headers, params: { offset, limit } })
      return productRes.data.results
    }

  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
