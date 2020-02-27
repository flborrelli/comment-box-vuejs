<template>

  <div>
  <nav class="navbar navbar-light">
  <a class="navbar-brand" href="#">
    <img src="/images/logo.png" class="d-inline-block align-center" alt="vue">
    Vue.js Comment App
  </a>
  </nav>
  <div class="container mt-2">
    <h2>Let us know your thoughts about Vue.js</h2>
    <hr />
    <FormToDo v-on:add-todo='addComment'/>
    <div class="list-group">
      <p v-if='commentsArray.length <= 0'>No comments yet...</p>
      <div class="list-group-item" v-for="(comment, idx) in allComments" v-bind:key="comment">
        <span class="comment_author">
          <strong>{{ comment.name }}</strong>
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

<style>

  .container h2 {
    color: darkslategray;
    text-align: center;
  }

  .navbar {
    background-color: rgba(219, 236, 193, 0.9);
    box-shadow: 0px 2px 2px 0px rgba(66, 65, 65, 0.75);
  }

  .navbar-brand {
    font-size: 25px;
    color: mediumseagreen !important;
  }

  .navbar-brand img {
    width: 5vw;
  }
</style>