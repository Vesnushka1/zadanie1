<template>
  <div>
    <CommentsSorted @sendValue="updateValueSelect" :sortedOptions="sortedOptions"/>
    <!--это пропс :sortedOptions(так называется в другом компоненте пропс)="sortedOptions"-->
    <SearchComments @searchValue="updateValueSearch"/>
    <MyButton @click="openModal">Открыть модальное окно</MyButton>
    <dialog :open="openDialog">
        <ModalAdd @close="closeWind" @create="addComment"/>
    </dialog>
    <ListComments @delete="delCommentApp" :comments="searchPosts"/>
  </div>
</template>

<script>

import ListComments from "@/components/ListComments";
import ModalAdd from "@/UI/ModalAdd";
import MyButton from "@/UI/MyButton";
import CommentsSorted from "@/UI/CommentsSorted";
import SearchComments from "@/UI/SearchComments";

export default {
  components: {MyButton, ModalAdd, ListComments, CommentsSorted, SearchComments},
  data() {
    return {
      posts: [],
      openDialog: false,
      sortedOptions: [
        {value: 'name', name: 'По возрастанию name'},
        {value: 'nameReverse', name: 'По убыванию name'},
        {value: 'email', name: 'По возрастанию email'},
        {value: 'emailReverse', name: 'По убыванию email'},
        {value: 'body', name: 'По возрастанию body'},
        {value: 'bodyReverse', name: 'По убыванию body'}
      ],
      selectValue: '',

      searchValue: ''
    }
  },
  methods: {
    async getPosts() {
      let res = await fetch('https://jsonplaceholder.typicode.com/comments')
      this.posts = await res.json()
    },
    delCommentApp(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    addComment(post) {
      this.posts.push(post)
    },
    openModal() {
      this.openDialog = !this.openDialog
    },
    closeWind(value) {
      this.openDialog = value
    },
    updateValueSelect(value) {
      this.selectValue = value
    },
    updateValueSearch(value) {
      this.searchValue = value
    },
  },
  computed: {
    sortedPosts() {
      if (this.selectValue.includes('Reverse')) {
        return [...this.posts].sort((post1, post2) => post1[this.selectValue.replace('Reverse', '')]?.localeCompare(post2[this.selectValue.replace('Reverse', '')])).reverse()
      } else {
        return [...this.posts].sort((post1, post2) => post1[this.selectValue]?.localeCompare(post2[this.selectValue]))
      }
    },
    searchPosts(){
      return this.sortedPosts.filter(obj => obj.name.toLowerCase().includes(this.searchValue.toLowerCase()) || obj.email.toLowerCase().includes(this.searchValue.toLowerCase()) || obj.body.toLowerCase().includes(this.searchValue.toLowerCase()))
    }
  },
  mounted() {
    this.getPosts()
  }
}
</script>

<style scoped>

</style>