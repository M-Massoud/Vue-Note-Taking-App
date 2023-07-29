<script setup>
const props = defineProps(['notes']);
const emits = defineEmits(['edit-note', 'delete-note']);

function handleEditNote(note) {
  emits('edit-note', note);
}

function handleDeleteNote(note) {
  emits('delete-note', note);
}
</script>

<template>
  <Transition name="switch" mode="out-in" appear>
    <p class="first-note-text" v-if="notes.length == 0">
      You don't have any notes yet!
    </p>
    <div v-else class="notes-container">
      <TransitionGroup name="fade" tag="" appear>
        <div v-for="note in notes" class="note-card" :key="note.id">
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
      </TransitionGroup>
    </div>
  </Transition>
</template>

<style scoped>
.notes-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  display: relative; /* for the animation */
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

.fade-enter-from,
.switch-enter-from {
  opacity: 0;
}
.fade-enter-to,
.switch-enter-to {
  opacity: 1;
}
.fade-enter-active,
.switch-enter-to {
  transition: all 0.3s ease;
}

.fade-leave-from,
.switch-leave-from {
  opacity: 1;
}
.fade-leave-to,
.switch-leave-to {
  opacity: 0;
}
.fade-leave-active,
.switch-leave-active {
  transition: all 0.3s ease;
}

.fade-leave-active {
  position: absolute;
}

.fade-move,
.switch-move {
  transition: all 0.3s ease;
}
</style>
