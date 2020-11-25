<template>
  <div>
    <div v-for="post in posts"
         class="post"
         :key="post.id">
      <h1>{{post.title}}</h1>
      <h2 @click="getUser(post.user_id)">User id: {{post.user_id}}</h2>
      <div v-for="comment in post.comments" class="comment">
        <h3>{{comment.name}}</h3>
        <h6>{{comment.email}}</h6>
        <p>{{comment.body}}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';

export default {
  data() {
    return {
      posts: [],
      user: null, 
      page: 1
    }
  },
  created () {
    this.getPosts();
  },
  methods: {
    getPosts() {
      this.$axios.get('posts', {
        params: {
          page: this.page 
        }
      }).then((response) => {
        this.posts = response.data.data
        this.posts.forEach(post => {
          this.$axios.get('comments', {
            params: {
              post_id: post.id
            }
          }).then((response) => {
            Vue.set(post, 'comments', response.data.data)
          })
        })
      })
    },
    getUser(userId) {
      this.$router.push('users/' + userId)
      this.$axios.get('users/' + userId).then((response) => {
        this.user = response.data.data
        window.alert(this.user.name)
      })
    }
  }
}
</script>

<style>
.post {
  border: 1px solid black;
}

.comment {
  border: 1px solid red;
}
</style>
