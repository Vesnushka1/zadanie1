<template>
  <select @change="selectVal">
    <option disabled selected>Выберите значение сортировки</option>
    <option v-for="option in sortedOptions" :value="option.value" :key="option.value"> {{ option.name }}</option>
    <option>По умолчанию</option>
  </select>
</template>

<script>
export default {
  props: {
    sortedOptions: {
      type: Array
    }
  },
  methods:{
    selectVal(event){
      this.$emit('sendValue', event.target.value)
    }
  }
}
</script>

<style scoped>
select{
  margin-bottom: 20px;
}
</style>