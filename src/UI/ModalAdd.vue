<template>
  <form class="formModal">
    <div class="content">
      <input placeholder="Введите имя" type="text" name="" id="" v-model="nameComment">
      <input placeholder="Введите email" type="email" name="" id="" v-model="emailComment">
      <input placeholder="Введите комментарий" type="text" name="" id="" v-model="bodyComment">
      <my-button @click.prevent='addComment'>Добавить</my-button>
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
      this.closeWindow()
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