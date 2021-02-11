<template>
  <b-container id="footer" fluid class="text-center">
    <div class="mx-auto" my-auto>{{ new Date().getFullYear() }} Copyright. NotNuts.com</div>
  </b-container>
</template>

<script>
export default {
  name: 'Footer',
  components: {
  },
  data () {
    return {

    }
  },
  methods: {

  }
}
</script>

<style scoped>
#footer {
  background: #304d79;
  height: 3rem;
  margin-top: 2rem;
}
div {
  display: flex;
  color: white;
  font-size: small;
  margin: auto 0 auto auto;
}
</style>
