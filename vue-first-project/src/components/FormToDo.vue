<template>
  <div class="form-todo form-group">
      <p>
        <input
          v-model="name"
          type="text"
          placeholder="Name"
          name="author"
          class="form-control"
        />
      </p>
      <p>
        <textarea
          v-model="message"
          name="message"
          class="form-control"
          placeholder="Your message here"
        >
        </textarea>
      </p>
      <button v-on:click="addComment" class="btn btn-primary">Comment</button>
    </div>
</template>

<script>
export default {
  data(){
    return {
      name: '',
      message: ''
    }
  },
  methods: {
    addComment(){
          if (this.message.trim() === ''){
            return;
          }
          this.$emit('add-todo', {
            name: this.name,
            message: this.message,
          })
          //To come back as a blank
          this.name = '';
          this.message = '';
        },
  }
}
</script>