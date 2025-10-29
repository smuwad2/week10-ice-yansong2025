<script>
import axios from 'axios'
import BlogPost from './subcomponents/BlogPost.vue'

export default {
  name: 'Ex2',
  components: { BlogPost },
  data() {
    return { posts: [] }
  },
  computed: {
    baseUrl() {
      if (window.location.hostname === 'localhost') {
        return 'http://localhost:3000'
      } else {
        const codespace_host = window.location.hostname.replace('5173', '3000')
        return `https://${codespace_host}`
      }
    }
  },
  created() {
    axios.get(`${this.baseUrl}/posts`)
      .then(res => { this.posts = res.data })
      .catch(err => {
        this.posts = [{
          id: 'error',
          subject: 'Error loading posts',
          entry: 'There was an error: ' + err.message,
          mood: 'sad'
        }]
      })
  }
}
</script>

<template>
  <div>
    <BlogPost
      v-for="post in posts"
      :key="post.id"
      :subject="post.subject"
      :entry="post.entry"
      :mood="post.mood"
    />
  </div>
</template>