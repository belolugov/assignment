<template>
  <div id="gallery" class="desktop">
    <div
      v-for="product in products"
      :key="product.id"
      @click="showModal(product)"
      v-b-modal="'modal'"
      class="product-card">
      <img :src="product.masterData.current.masterVariant.images.length > 0 ? product.masterData.current.masterVariant.images[0].url : 'https://1b0bbb9e89b4713adcc7-aea4cee2cb18344b328e3a03eff3ec4f.ssl.cf1.rackcdn.com/ece4edb2868a8225.cro-U2aFaCJE-thumb.jpg'">
      <div class="info">
        <h5>{{ product.masterData.current.name.en }}</h5>
        <hr>
      </div>
    </div>
    <Modal :modalInfo="modalInfo"/>
  </div>
</template>

<script>
import Modal from './Modal.vue'
export default {
  name: 'Gallery',
  props: ['products'],
  components: {
    Modal
  },
  data () {
    return {
      modalInfo: null
    }
  },
  methods: {
    showModal (product) {
      this.modalInfo = product
      this.$bvModal.show('modal')
    }
  }
}
</script>

<style scoped>
.desktop {
  max-width: 960px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(150px, auto);
  grid-gap: 30px;
  padding: 5rem 30px 30px;
}
.desktop img {
  width: 90%;
  max-height: 50%;
  align-self: center;
}

.desktop .wrapper {
  grid-column: 1/5;
  width: 50%;
  margin: auto;
}

hr {
  border-top-width:2px;
}
.mobile img {
  width: 90%;
  max-height: 100%;
}
.mobile .info {
  margin-top: 50px;
}
.product-card{
  display: inline-grid;
  transition: all .2s ease-in-out;
}
.info{
  align-self: end;
}
.info p {
  font-size: medium;
}
.product-card:hover{
  cursor:pointer;
  transform: scale(1.2);
}
a:hover{
  text-decoration: none;
}
</style>
