// main.js
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')

// App.vue
<template>
  <div id="app">
    <h1>Daftar Kegiatan</h1>
    <input v-model="newActivity" @keyup.enter="addActivity">
    <button @click="addActivity">Tambah Kegiatan</button>
    <ul>
      <li v-for="(activity, index) in filteredActivities" :key="index" :class="{ done: activity.done }">
        <input type="checkbox" v-model="activity.done">
        <span>{{ activity.name }}</span>
        <button @click="removeActivity(index)">Hapus</button>
      </li>
    </ul>
    <button @click="toggleFilter">Tampilkan Belum Selesai</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: '',
      activities: [],
      showOnlyIncomplete: false
    }
  },
  methods: {
    addActivity() {
      this.activities.push({ name: this.newActivity, done: false });
      this.newActivity = '';
    },
    removeActivity(index) {
      this.activities.splice(index, 1);
    },
    toggleFilter() {
      this.showOnlyIncomplete = !this.showOnlyIncomplete;
    }
  },
  computed: {
    filteredActivities() {
      if (this.showOnlyIncomplete) {
        return this.activities.filter(activity => !activity.done);
      } else {
        return this.activities;
      }
    }
  }
}
</script>

<style>
.done {
  text-decoration: line-through;
}
</style>
