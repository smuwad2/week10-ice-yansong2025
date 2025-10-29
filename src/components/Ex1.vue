<script>
import SoundIcon from './subcomponents/SoundIcon.vue'; // path from Ex1.vue

export default {
  name: 'Ex1',
  components: { SoundIcon },
  data() {
    return { soundLevel: 0 };
  }
};
</script>

<template>
  <div>
    <label>
      Sound level
      <input type="number" min="0" max="3" v-model.number="soundLevel" />
    </label>

    <!-- Remove the wrapper <span class="ms-2"> -->
    <SoundIcon :level="soundLevel" />
  </div>
</template>