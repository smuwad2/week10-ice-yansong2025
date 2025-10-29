<script>
export default {
  props: {
    level: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      soundEmojis: ['🔇', '🔈', '🔉', '🔊']
    }
  }
}
</script>

<template>
  <!-- show emoji based on prop level -->
  <span>{{ soundEmojis[level] }}</span>
</template>