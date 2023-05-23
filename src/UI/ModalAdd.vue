<template>
  <form class="formModal">
    <div class="content">
      <input type="text" name="" id="" v-model="nameComment">
      <input type="email" name="" id="" v-model="emailComment">
      <input type="text" name="" id="" v-model="bodyComment">
      <my-button @click='addComment'>Добавить</my-button>
    </div>
    <button @click.prevent="closeWindow" class="btn-close">X</button>

  </form>
</template>

<script>
import MyButton from "@/UI/MyButton";

export default {
  components: {MyButton},
  data() {
    return {
      nameComment: '',
      emailComment: '',
      bodyComment: '',
    }
  },
  methods: {
    addComment() {
      let post = {
        name: this.nameComment,
        email: this.emailComment,
        body: this.bodyComment
      }
      post.id = Date.now()
      this.$emit('create', post)
      this.nameComment = ''
      this.emailComment = ''
      this.bodyComment = ''
    },
    closeWindow(){
      this.$emit('close', false)
    }
  }
}
</script>

<style scoped>
.formModal{
  display: flex;
}
.content{
  display: flex;
  flex-direction: column;
}
.btn-close{
  width: 40px;
  height: 30px;
}
</style>