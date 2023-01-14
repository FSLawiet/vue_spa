<script>
import CommentForm from "./CommentForm";
export default {
  components: {
    CommentForm,
  },
  data() {
    return {
      comments: [],
    };
  },
  watch: {
    comments: {
      deep: true,
      handler(val) {
        console.info(val);
      },
    },
  },
  methods: {
    addComment(comment) {
      let { comments } = this;
      comments.push(comment);
    },
    deleteComment(index) {
      let { comments } = this;
      comments.splice(index, 1);
    },
  },
  computed: {
    allComments() {
      let { comments } = this;
      return comments.map((comment) => ({
        ...comment,
        author: comment.author.trim() === "" ? "Anônimo" : comment.author,
      }));
    },
  },
};
</script>

<template>
  <div class="container">
    <h1 id="title">Comentários</h1>
    <hr />
    <CommentForm @add-comment="addComment" />
    <hr />
    <div class="list-group">
      <p v-if="comments.length <= 0">Sem comentários...</p>
      <div
        v-else
        class="list-group-item"
        v-for="(comment, index) in allComments"
        :key="index"
      >
        <span class="comment__author">
          Autor: <strong>{{ comment.author }}</strong>
        </span>
        <p>{{ comment.message }}</p>
        <div>
          <a href="#" title="Excluir" @click.prevent="deleteComment(index)"
            >Excluir</a
          >
        </div>
      </div>
    </div>
    <hr />
  </div>
</template>

<style></style>
