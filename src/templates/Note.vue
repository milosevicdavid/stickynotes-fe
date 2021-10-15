<template>
  <div class="model-wrapper">
    <div class="model">
      <b-field label="Title:">
        <b-input v-model="note.title"></b-input>
      </b-field>

      <b-field label="Note:">
        <b-input
          v-model="note.content"
          maxlength="10000"
          type="textarea"
        ></b-input>
      </b-field>
      <div class="buttons-wrapper">
        <div class="color">
          <div class="color-text">Color:</div>
          <div
            @click="changeColor('is-default')"
            class="color-button is-default"
            :class="{ 'is-border': note.color === 'is-default' }"
          ></div>

          <div
            @click="changeColor('is-danger')"
            class="color-button is-danger"
            :class="{ 'is-border': note.color === 'is-danger' }"
          ></div>
          <div
            @click="changeColor('is-success')"
            class="color-button is-success"
            :class="{ 'is-border': note.color === 'is-success' }"
          ></div>
          <div
            @click="changeColor('is-info')"
            class="color-button is-info"
            :class="{ 'is-border': note.color === 'is-info' }"
          ></div>
          <div
            @click="changeColor('is-warning')"
            class="color-button is-warning"
            :class="{ 'is-border': note.color === 'is-warning' }"
          ></div>
        </div>
        <div class="confirm-buttons">
          <b-button @click="editNote" class="buttons" type="is-dark"
            >Save</b-button
          >
          <b-button @click="cancelEdit" class="buttons" type="is-dark"
            >Cancel</b-button
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { animate } from "motion";

export default {
  data() {
    return {
      note: {}
    };
  },
  mounted() {
    const { id } = this.$route.params;
    fetch(`http://localhost:8000/${id}`)
      .then(response => response.json())
      .then(data => (this.note = data));
  },

  methods: {
    editNote() {
      if (this.note.title === "") {
        this.$buefy.dialog.alert("You cannot confirm note without a title");
      } else {
        const { id } = this.$route.params;
        fetch(`http://localhost:8000/${id}`, {
          method: "PUT",
          body: JSON.stringify(this.note)
        }).then(() => this.$router.push("/notes"));
      }
    },
    cancelEdit() {
      this.$router.push("/notes");
    },
    changeColor(color) {
      this.note.color = color;
      const otherArray = [];
      for (let i = 0; i < 5; i++) {
        const otherclass = document.getElementsByClassName("color-button")[i]
          .classList[1];
        if (otherclass !== color) {
          otherArray.push(otherclass);
        }
      }
      if (this.note.color === color) {
        animate(`.${color}`, { transform: "rotate(45deg)" }, { duration: 0.5 });
      }
      for (let j = 0; j < otherArray.length; j++) {
        animate(
          `.${otherArray[j]}`,
          { transform: "rotate(0deg)" },
          { duration: 0.5 }
        );
      }
    }
  }
};
</script>

<style>
.model-wrapper {
  display: flex;
  justify-content: center;
  text-align: left;
}

.color-button {
  height: 30px;
  width: 30px;
  border-radius: 20%;
  margin: 0px 5px;
  cursor: pointer;
}

.color {
  display: flex;
  align-items: center;
}

.color-text {
  color: white;
  margin-right: 10px;
}

.buttons {
  margin: 4px;
  width: 80px;
  text-align: center;
}

.confirm-buttons {
  display: flex;
}

.buttons-wrapper {
  display: flex;
  justify-content: space-around;
}

.model {
  width: 800px;
}

.is-danger {
  background-color: #f14668;
}

.is-success {
  background-color: #48c78e;
}

.is-info {
  background-color: #3e8ed0;
}

.is-warning {
  background-color: #ffe08a;
}

.is-border {
  border: 1px solid white;
}
</style>
