<script setup>
defineProps(['notes']);
</script>

<template>
  <div class="notes-container">
    <div class="first-note-text" v-if="notes.length == 0">
      You don't have any notes yet!
    </div>
    <div v-for="note in notes" class="note-card">
      <h2>{{ note.title }}</h2>
      <p>{{ note.content }}</p>
    </div>
  </div>
</template>

<style scoped>
.notes-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.first-note-text {
  color: var(--grey-color);
}

.note-card {
  background-color: var(--darker-black);
  color: var(--grey-color);
  border-radius: 4px;
  padding: 16px;
  margin: 12px;
}
</style>
