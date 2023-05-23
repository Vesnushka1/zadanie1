<template>
  <input @input="searchValue" type="text">
</template>

<script>
export default {
  methods:{
    searchValue(event){
      this.$emit('searchValue', event.target.value)
    }
  }
}
</script>

<style scoped>

</style>