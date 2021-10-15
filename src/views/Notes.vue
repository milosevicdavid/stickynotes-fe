<template>
  <div>
    <div class="notes-wrapper">
      <div v-for="note in notes" :key="note.id">
        <div class="note">
          <b-message
            :title="note.title"
            :type="note.color"
            @close="removeNote(note.id)"
          >
            <div class="content">{{ note.content }}</div>
            <router-link :to="{ name: 'Note', params: { id: note.id } }"
              ><b-button :type="note.color">Edit</b-button></router-link
            >
          </b-message>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      notes: []
    };
  },
  mounted() {
    fetch("http://localhost:8000/")
      .then(response => response.json())
      .then(data => (this.notes = data));
  },
  methods: {
    removeNote(id) {
      fetch(`http://localhost:8000/${id}`, {
        method: "delete"
      });
    }
  }
};
</script>

<style>
.notes-wrapper {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  flex-direction: row-reverse;
}

.note {
  width: 320px;
  margin: 20px;
}

.content {
  padding: 15px;
}
</style>
