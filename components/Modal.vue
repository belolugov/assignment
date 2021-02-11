<template>
  <div>
    <b-modal id="modal" :title="info.name">
      <img v-if="info.organic" class="organic" src="https://1b0bbb9e89b4713adcc7-aea4cee2cb18344b328e3a03eff3ec4f.ssl.cf1.rackcdn.com/5e85d71501308335-L2AE6hCf-thumb.jpg" alt="">
      <img :src="info.image" alt="">
      <p>{{ info.description }}</p>
      <p>{{ info.price }}</p>
    </b-modal>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  props: ['modalInfo'],
  data () {
    return {}
  },
  computed: {
    info () {
      if (!this.modalInfo) {
        return {}
      } else {
        const images = this.modalInfo.masterData.current.masterVariant.images
        let modalImage = null
        switch (images.length) {
          case 2: {
            modalImage = images[1].url
            break
          }
          case 1: {
            modalImage = images[0].url
            break
          }
          default: {
            modalImage = 'https://1b0bbb9e89b4713adcc7-aea4cee2cb18344b328e3a03eff3ec4f.ssl.cf1.rackcdn.com/ece4edb2868a8225.cro-U2aFaCJE.jpg'
          }
        }
        let modalPrice = 'N/A'
        if (this.modalInfo.masterData.current.masterVariant.prices.length > 0) {
          modalPrice = '$' + this.modalInfo.masterData.current.masterVariant.prices[0].value.centAmount / 100
        }
        let badge = null
        if (this.modalInfo.masterData.current.masterVariant.attributes.length > 1) {
          badge = this.modalInfo.masterData.current.masterVariant.attributes[1].value
        }
        return {
          name: this.modalInfo.masterData.current.name.en,
          image: modalImage,
          description: this.modalInfo.masterData.current.description.en,
          price: modalPrice,
          organic: badge
        }
      }
    }
  }
}

</script>

<style>
  #modal {
    text-align: center;
  }
  .modal-header {
    text-align: center;
  }
  img {
    width: 95%;
  }
  .organic {
    width: 10%;
    float: right;
    display: block;
  }

</style>
