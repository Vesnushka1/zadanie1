<template>
  <div>
    <PostComment @delete="delComment" v-for="comment in comments" :key="comment.id" :comment="comment"/>
  </div>
</template>

<script>
import PostComment from "@/components/PostComment";

export default {
  components: {
    PostComment
  },

  props: {
    comments: {
      type: Array,
    }
  },
  methods: {
    delComment(post) {
      this.$emit('delete', post)
    }
  }
}
</script>

<style scoped>

</style>