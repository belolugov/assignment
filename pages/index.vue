<template>
  <h1>Index Page</h1>
</template>

<script>
export default {
  middleware ({ redirect }) {
    return redirect('/shop')
  }
}
</script>
