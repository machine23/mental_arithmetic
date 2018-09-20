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
    <div class="settings">
      <div><label>Min: <input type="number" v-model.number="min"></label></div>
      <div><label>Max: <input type="number" v-model.number="max"></label></div>
    </div>
    <question @success="onSuccess" @onError="onError" :min="min" :max="max"/>
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
      errors: 0,
      min: 0,
      max: 100,
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
.settings {
  display: flex;
  max-width: 300px;
  justify-content: center;
  margin: 30px auto;
}
.settings input {
  border: none;
  outline: none;
  border-bottom: 1px solid #eee;
  width: 100px;
  font-size: 18px;
  color: #2c3e50;
  text-align: center;
}
</style>
