<script>
export default {
  name: 'BlogPost2',
  props: {
    subject: {
      type: String,
      required: true
    },
    entry: {
      type: String,
      required: true
    },
    mood: {
      type: String,
      required: false,
      default: 'happy'
    }
  },
  computed: {
    moodImage() {
      // Prevent runtime error if mood is undefined
      const safeMood = (this.mood || 'happy').toLowerCase()
      return `/assets/${safeMood}.png`
    }
  }
}
</script>

<template>
  <div class="card mb-3 text-center shadow-sm" style="width: 18rem; margin: auto;">
    <img
      :src="moodImage"
      class="card-img-top"
      alt="Mood image"
      style="max-height: 180px; object-fit: contain;"
    />
    <div class="card-body">
      <h5 class="card-title">{{ subject }}</h5>
      <p class="card-text">{{ entry }}</p>
    </div>
  </div>
</template>