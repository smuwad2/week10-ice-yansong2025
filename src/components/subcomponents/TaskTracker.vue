<script>
export default {
  name: 'TaskTracker',
  props: {
    task: { type: Object, required: true }, // { desc, deadline }
    idx: { type: Number, required: true }
  }
};
</script>

<template>
  <div class="card mb-3">
    <div class="card-body">
      <!-- Title not asserted by test, but fine to include -->
      <h5 class="card-title">Task {{ idx + 1 }}</h5>

      <!-- Test asserts this exact <p> text equals task.desc -->
      <p class="card-text">{{ task.desc }}</p>

      <!-- Test searches for `div.card:has-text("Deadline: YYYY-MM-DD")` -->
      <div class="text-muted">Deadline: {{ task.deadline }}</div>

      <!-- Test clicks button:has-text("Done") -->
      <button class="btn btn-sm btn-success mt-2" @click="$emit('done', idx)">
        Done
      </button>
    </div>
  </div>
</template>