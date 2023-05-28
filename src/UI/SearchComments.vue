<template>
  <input placeholder="Поиск" @input="searchValue" type="text">
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
input{
  width: 170px;
  height: 25px;
}
</style>