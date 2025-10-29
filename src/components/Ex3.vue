<script>
import axios from 'axios';
import BlogPost from './subcomponents/BlogPost2.vue';

export default {
  name: 'Ex3',
  components: { BlogPost },
  data() {
    return {
      posts: []
    };
  },
  computed: {
    baseUrl() {
      if (window.location.hostname === 'localhost') {
        return 'http://localhost:3000';
      } else {
        const codespace_host = window.location.hostname.replace('5173', '3000');
        return `https://${codespace_host}`;
      }
    }
  },
  created() {
    // Initial fetch so count matches server right after mount
    axios.get(`${this.baseUrl}/posts`)
      .then(res => { this.posts = res.data; })
      .catch(err => {
        this.posts = [{
          id: 'error',
          subject: 'Error loading posts',
          entry: 'There was an error: ' + err.message,
          mood: 'sad'
        }];
      });
  },
  methods: {
    async deletePost(id) {
      try {
        // Match course/test backend style: GET /deletePost?id=...
        await axios.get(`${this.baseUrl}/deletePost`, { params: { id } });

        // Update local state so UI count matches new server count
        this.posts = this.posts.filter(p => p.id !== id);
      } catch (err) {
        console.error('Error deleting post:', err);
        alert('Failed to delete post: ' + err.message);
      }
    }
  }
};
</script>

<template>
  <div>
    <h2 class="mb-3">Blog Posts</h2>

    <div v-for="p in posts" :key="p.id" class="mb-3">
      <BlogPost :subject="p.subject" :entry="p.entry" :mood="p.mood" />
      <button
        v-if="p.id !== 'error'"
        class="btn btn-sm btn-danger mt-2"
        @click="deletePost(p.id)"
      >
        Delete
      </button>
    </div>
  </div>
</template>