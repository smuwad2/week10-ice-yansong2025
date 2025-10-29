<script>
import TaskTracker from './subcomponents/TaskTracker.vue';

export default {
  name: 'Ex4',
  components: { TaskTracker },
  data() {
    return {
      desc: '',
      deadline: '',
      tasks: [] // each: { desc, deadline }
    };
  },
  methods: {
    addTask() {
      // keep it simple; tests always provide both fields
      if (!this.desc || !this.deadline) return;
      this.tasks.push({ desc: this.desc, deadline: this.deadline });
      // clear inputs for next entry (not required by test, but nice)
      this.desc = '';
      this.deadline = '';
    },
    removeTask(idx) {
      this.tasks.splice(idx, 1);
    }
  }
};
</script>

<template>
  <div>
    <!-- Test locates these by type -->
    <input type="text" v-model="desc" placeholder="Task description" />
    <input type="date" v-model="deadline" />

    <!-- Test queries by role+name: button "Add New Task" -->
    <button @click="addTask">Add New Task</button>

    <!-- Render cards -->
    <TaskTracker
      v-for="(t, i) in tasks"
      :key="i"
      :task="t"
      :idx="i"
      @done="removeTask"
    />
  </div>
</template>