<script setup>
const props = defineProps(['notes']);
const emits = defineEmits(['delete-note']);

function handleDeleteNote(note) {
  emits('delete-note', note);
}
</script>

<template>
  <div class="notes-container">
    <div class="first-note-text" v-if="notes.length == 0">
      You don't have any notes yet!
    </div>
    <div v-for="note in notes" class="note-card">
      <h2>{{ note.title }}</h2>
      <p>{{ note.content }}</p>
      <div class="note-card-actions-container">
        <font-awesome-icon
          class="note-card-action"
          @click="handleEditNote(note)"
          icon="fa-solid fa-pen-to-square"
        />
        <font-awesome-icon
          class="note-card-action"
          @click="handleDeleteNote(note)"
          icon="fa-solid fa-trash"
        />
      </div>
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

.note-card-actions-container {
  margin-top: 16px;
  display: flex;
  justify-content: flex-end;
  gap: 12px;
}

.note-card-action {
  cursor: pointer;
}
</style>
