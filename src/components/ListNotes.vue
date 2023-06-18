<script setup>
defineProps(['notes']);
</script>

<template>
  <div class="notes-container">
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
  gap: 2%;
}

.note-card {
  background-color: var(--darker-black);
  color: var(--grey-color);
  border-radius: 4px;
  padding: 16px;
  margin-bottom: 2%;
}
</style>
