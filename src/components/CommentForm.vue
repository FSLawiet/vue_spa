<script>
export default {
  data() {
    return {
      author: "",
      message: "",
    };
  },
  methods: {
    addComment() {
      let { author, message, $emit, clearFields } = this;
      if (!message) alert("Preencha o comentário!");
      else {
        $emit("add-comment", { author, message });
        clearFields();
      }
    },
    clearFields() {
      this.author = "";
      this.message = "";
    },
  },
};
</script>
<template>
  <div class="form-todo form-group">
    <p>
      <input
        placeholder="Nome"
        type="text"
        name="author"
        class="form-control"
        v-model="author"
      />
    </p>
    <p>
      <textarea
        placeholder="Comentário"
        name="message"
        id="comentario"
        cols="30"
        rows="10"
        class="form-control"
        v-model="message"
      ></textarea>
    </p>
    <button @click="addComment" type="submit" class="btn btn-primary">
      Comentar
    </button>
  </div>
</template>
