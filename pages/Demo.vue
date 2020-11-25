<template lang="html">
  <div class="wrapper">
    <button class="change__style" @click="changeStyle()">
      Change style
    </button>
    <tabs
      :mode="mode"
    >
      <tab title="Users">
      </tab>
      <tab title="Comments">
      </tab>
      <tab title="Posts">
      </tab>
    </tabs>
  </div>
</template>

<script>
import test from './test.vue'
import users from '../users/_id.vue'
import axios from 'axios'

export default {
  components: {
    test,
    Users,
  },
  data () {
    return {
      mode: 'dark',
    }
  },
  created () {
    this.getUser()
    this.getComments()
    this.getPosts()
  },
  methods: {
    changeStyle () {
      if (this.mode === 'dark') {
        this.mode = 'light'
      } else {
        this.mode = 'dark'
      }
    },
    getUser () {
      this.$axios.get('users').then((response) => {
        this.user = response.data
      })
    },
    getComments () {
      this.$axios.get('comments').then((response) => {
        this.comments = response.data
      })
    },
    getPosts () {
      this.$axios.get('posts').then((response) => {
        this.posts = response.data
      })
    }
  }
}
</script>

<style lang="css">
  * {
    margin: 0;
    padding: 0;
    font-family: 'Karla', sans-serif;
  }
  .wrapper {
    width: 100%;
    min-height: 100vh;
    background-color: #f8f8f8;
    margin: 0;
    padding: 20px;
  }

  .change__style {
    background-color: #eee;
    font-size: 1em;
    margin-bottom: 10px;
    padding: 5px;
  }
</style>
