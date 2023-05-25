<template>
    {{ address.street +" "+ address.number }} //displays streetname and number
</template>

<script>
export default {
  props: {
    address: {}
  }
}
</script>

<style>

</style>