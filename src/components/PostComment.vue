<template>
  <div class="comm">
    <p>{{ comment.name }}</p>
    <p>{{ comment.email }}</p>
    <p>{{ comment.body }}</p>
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
}
</style>