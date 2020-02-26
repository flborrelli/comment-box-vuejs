<template>
  <div class="container">
    <h1>Comments</h1>
    <hr />
    <FormToDo v-on:add-todo='addComment'/>
    <div class="list-group">
      <p v-if='commentsArray.length <= 0'>No comments yet...</p>
      <div class="list-group-item" v-for="(comment, idx) in allComments" v-bind:key="comment">
        <span class="comment_author">
          Author: <strong>{{ comment.name }}</strong>
        </span>
        <p>{{ comment.message }}</p>
        <div>
          <a v-on:click.prevent="deleteComment(idx)" href="#" title="Delete"
            >Delete</a
          >
        </div>
      </div>
    </div>
    <hr />
  </div>
</template>

<script>
import FormToDo from './FormToDo';

export default {
  components: {
    FormToDo
  },

data() {
        return {
          commentsArray: [],
          name: '',
          message: ''
        };
      },
      methods: {
        addComment(comment){
          this.commentsArray.push(comment);
        },
        deleteComment(idx){
          this.commentsArray.splice(idx, 1);
        }
      },
      computed: {
        allComments(){
          return this.commentsArray.map(comment => (
            {
              ...comment, //spread operator to get all properties from the respective comment, specifying name as follows
              name: comment.name.trim() === '' ? 'Anonymous' : comment.name
          }))
        }
      },
      watch: {
        commentsArray(val){
          console.log('val', val)
        }
      }
}
</script>
