<script setup>
import { ref } from 'vue';

const showModal = ref(false);
const notes = ref([]);

function openModal() {
  showModal.value = true;
}

function closeModal() {
  showModal.value = false;
}
</script>

<template>
  <button class="modal-open-button" @click="openModal">
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
      <input class="modal-form-input" id="note-title" />

      <p class="modal-form-label">
        <label for="note-content">Note Content</label>
      </p>
      <textarea class="modal-form-text-area" id="note-content" rows="8" cols="48" />
    </form>
  </div>
</template>

<style scoped>
.note-modal {
  background-color: #1a1a1a;
  position: relative;
  padding: 24px;
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
