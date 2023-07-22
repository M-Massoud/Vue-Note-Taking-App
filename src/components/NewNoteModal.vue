<script setup>
import { ref, watch, onMounted } from 'vue';
import ListNotes from './ListNotes.vue';

const showModal = ref(false);
const editModal = ref(false);
const note = ref({ id: '', title: '', content: '' });
const notes = ref(
  localStorage.getItem('notes') ? JSON.parse(localStorage.getItem('notes')) : []
);
let selectedNoteId = '';

function openAddNoteModal() {
  editModal.value = false;
  showModal.value = true;
  note.value = { id: '', title: '', content: '' };
  selectedNoteId = '';
}

function closeModal() {
  showModal.value = false;
}

function confirmNote(event) {
  event.preventDefault();
  notes.value.push({
    id: Date.now(),
    title: note.value.title,
    content: note.value.content,
  });
  showModal.value = false;
  note.value = { title: '', content: '' };
}

function editNote(selectedNote) {
  editModal.value = true;
  showModal.value = true;
  selectedNoteId = selectedNote.id;
  note.value.title = selectedNote.title;
  note.value.content = selectedNote.content;
}

function confirmEditNote(event) {
  event.preventDefault();
  const noteIndex = notes.value.findIndex(
    currentNote => currentNote.id == selectedNoteId
  );
  showModal.value = true;
  notes.value[noteIndex] = {
    id: selectedNoteId,
    title: note.value.title,
    content: note.value.content,
  };
  selectedNoteId = '';
  showModal.value = false;
}

function deleteNote(note) {
  notes.value = notes.value.filter(currentNote => currentNote.id != note.id);
}

// onMounted(() => {
//   if (localStorage.getItem('notes')) {
//     notes.value = JSON.parse(localStorage.getItem('notes'));
//   }
// });

watch(
  notes,
  currentValue => {
    localStorage.setItem('notes', JSON.stringify(currentValue));
  },
  { deep: true }
);
</script>

<template>
  <ListNotes :notes="notes" @edit-note="editNote" @delete-note="deleteNote" />
  <button class="modal-open-button" @click="openAddNoteModal">
    <font-awesome-icon icon="plus" /> Add Note
  </button>

  <div v-if="showModal == true" class="note-modal card">
    <button class="modal-close-button" @click="closeModal">
      <font-awesome-icon icon="fa-solid fa-xmark" />
    </button>
    <form>
      <p class="modal-form-label">
        <label for="note-title">Note Title</label>
      </p>
      <input class="modal-form-input" id="note-title" v-model="note.title" />

      <p class="modal-form-label">
        <label for="note-content">Note Content</label>
      </p>
      <textarea
        class="modal-form-text-area"
        id="note-content"
        v-model="note.content"
        rows="8"
        cols="48"
      />

      <button
        class="modal-confirm-button"
        @click="editModal ? confirmEditNote($event) : confirmNote($event)"
        :disabled="note.title == '' || note.content == ''"
      >
        {{ editModal ? 'Confirm Edit' : 'Confirm' }}
      </button>
    </form>
  </div>
</template>

<style scoped>
.note-modal {
  background-color: #1a1a1a;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
  padding: 24px;
  width: 480px;
}

@media screen and (max-width: 992px) {
  .note-modal {
    max-width: 85%;
  }
}

.modal-open-button {
  position: fixed;
  top: 85%;
  right: 5%;
}

.modal-close-button {
  position: absolute;
  top: 16px;
  right: 8px;
}

.modal-confirm-button {
  margin-top: 16px;
  border: 1px solid transparent;
  background-color: var(--lighter-black);
}

.modal-confirm-button:disabled {
  background-color: var(--grey-color);
  color: var(--lighter-black);
  cursor: not-allowed;
}

.modal-form-label {
  text-align: left;
  margin-top: 20px;
  margin-bottom: 10px;
  color: var(--grey-color);
}

.modal-form-input,
.modal-form-text-area {
  display: block;
  background-color: #242424;
  color: rgba(255, 255, 255, 0.87);
  border-radius: 0.25rem;
  border: 1px solid transparent;
  width: 100%;
  padding: 8px 4px;
}
</style>
