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
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: space-around;
  gap: 1%;
}

.note-card {
  background-color: var(--darker-black);
  color: var(--grey-color);
  border-radius: 4px;
  padding: 16px;
  flex-basis: 30%;
}
</style>
