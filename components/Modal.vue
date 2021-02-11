<template>
  <div>
    <b-modal id="modal" :title="info.name">
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
      if (this.modalInfo === '') {
        return ''
      } else {
        console.log(this.modalInfo)
        return {
          name: this.modalInfo.masterData.current.name.en,
          image: this.modalInfo.masterData.current.masterVariant.images[0].url,
          description: this.modalInfo.masterData.current.description.en,
          price: '$' + this.modalInfo.masterData.current.masterVariant.prices[0].value.centAmount / 100,
          organic: this.modalInfo.masterData.current.masterVariant.attributes[1].value
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
</style>
