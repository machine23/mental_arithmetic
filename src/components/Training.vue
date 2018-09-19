<template>
  <div>
    <h1>Training</h1>
    <div class="info">
      <div>
        Correct: {{ correct }}
      </div>
      <div>
        Errors: {{ errors }}
      </div>
      <div>
        Time: 
      </div>
    </div>
    <question @success="onSuccess" @onError="onError"/>
    <button @click="$emit('onStop')">Stop</button>
  </div>
</template>

<script>
import Question from "./Question.vue";
export default {
  name: "Training",
  components: {
    Question
  },
  data() {
    return {
      correct: 0,
      errors: 0
    };
  },
  methods: {
    onSuccess() {
      this.correct++;
    },
    onError() {
      this.errors++;
    }
  }
};
</script>

<style>
.info {
  display: flex;
  max-width: 300px;
  margin: 30px auto;
  justify-content: space-between;
}
</style>
