<script>
export default {
  name: 'BlogPost',
  props: {
    subject: { type: String, required: true },
    entry:   { type: String, required: true },
    mood:    { type: String, default: 'happy' }
  },
  computed: {
    moodImage() {
      const safe = (this.mood || 'happy').toLowerCase()
      return `/assets/${safe}.png`
    }
  }
}
</script>

<template>
  <div class="card mb-3 text-center shadow-sm" style="width: 18rem;">
    <img class="card-img-top" :src="moodImage" :alt="mood" style="max-height:180px; object-fit:contain;">
    <div class="card-body">
      <h5 class="card-title">{{ subject }}</h5>
      <p class="card-text">{{ entry }}</p>
    </div>
  </div>
</template>