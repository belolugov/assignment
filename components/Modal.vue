<template>
  <div>
    <b-modal id="modal" :title="modalInfo==='' ? '' : modalInfo.masterData.current.name.en">
      <img :src="modalInfo==='' ? '' : modalInfo.masterData.current.masterVariant.images[0].url" alt="">
      <p>{{ modalInfo==='' ? '' : modalInfo.masterData.current.description.en }}</p>
    </b-modal>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  props: ['modalInfo'],
  data () {
    return {}
  }
}

</script>

<style>
  #modal {
    text-align: center;
  }
  img {
    width: 95%;
  }

</style>
