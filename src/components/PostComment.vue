<template>
  <div class="comm">
    <div class="text-comm"><strong>Name: </strong>{{ comment.name }}</div>
    <div class="text-comm"><strong>Email: </strong>{{ comment.email }}</div>
    <div class="text-comm"><strong>Comment: </strong>{{ comment.body }}</div>
    <my-button @click="delComment">Удалить</my-button>
  </div>
</template>

<script>
import MyButton from "@/UI/MyButton";

export default {
  components: {
    MyButton
  },

  props: {
    comment: {
      type: Object,
    }
  },
  methods: {
    delComment() {
      this.$emit('delete', this.comment)
    }
  }
}
</script>

<style scoped>
.comm {
  padding: 20px;
  margin: 10px;
  border: 2px solid black;
  width: 500px;
}
.text-comm{
  margin: 10px 0;
}
</style>