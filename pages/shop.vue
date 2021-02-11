<template>
  <div class="container">
    <Gallery :products="products"/>
  </div>
</template>

<script>
export default {
  data () {
    return {
      token: null,
      loadingProducts: false,
      products: []
    }
  },
  head () {
    return {
      title: 'Shop'
    }
  },
  async fetch () {
    await this.getToken().then((res) => {
      this.token = res
    })
    await this.getProducts().then((res) => {
      this.products = res
    })
  },
  mounted () {
    this.scroll()
  },
  methods: {
    async getToken () {
      const username = 'BZaa-av5L6RmZKlPgZaGNkea'
      const password = 'jchbf_Q5zRWCaEg4TCB4m9cLIioPiml0'
      const tokenUrl = 'https://auth.commercetools.co/oauth/token?grant_type=client_credentials&scope=view_products:nuts-custom-demo-1'
      const headers = {
        Authorization: 'Basic ' + Buffer.from(username + ':' + password).toString('base64')
      }
      const tokenRes = await this.$axios.post(tokenUrl, {},
        { headers })
      return tokenRes.data.access_token
    },
    async getProducts (offset = 0, limit = 12) {
      if (!this.token) {
        return []
      }
      const headers = {
        Authorization: 'Bearer ' + this.token
      }
      const productRes = await this.$axios.get('https://api.commercetools.co/nuts-custom-demo-1/products', {
        headers,
        params: {
          offset,
          limit
        }
      })
      return productRes.data.results
    },
    scroll () {
      window.onscroll = () => {
        const bottomOfWindow = document.documentElement.offsetHeight - (Math.max(window.pageYOffset, document.documentElement.scrollTop, document.body.scrollTop) + window.innerHeight)
        if (bottomOfWindow < 20) {
          if (!this.loadingProducts) {
            this.loadingProducts = true
            this.getProducts(this.products.length, 12).then((res) => {
              this.products.push(...res)
              this.loadingProducts = false
            })
          }
        }
      }
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
</style>
