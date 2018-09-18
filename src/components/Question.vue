<template>
  <form class="question__form" @submit.prevent="onSubmit">
    <label>
      {{ x }} + {{ y }} =
      <input type="text" v-model.number="userAnswer" autofocus>
    </label>
  </form>
</template>

<script>
function getRandomInt(min, max) {
  const diff = max - min;
  return Math.floor(Math.random() * diff) + min;
}

export default {
  name: "Question",
  data() {
    return {
      x: getRandomInt(0, 100),
      y: getRandomInt(0, 100),
      userAnswer: null
    };
  },
  computed: {
    answer() {
      return this.x + this.y;
    }
  },
  methods: {
    onSubmit() {
      console.log('submit');
      if (this.checkAnswer()) {
        console.log('good');
        this.renew();
      } else {
        console.log('not good');
      }
    },
    renew() {
      this.x = getRandomInt(0, 100);
      this.y = getRandomInt(0, 100);
      this.userAnswer = null;
    },
    checkAnswer() {
      return this.userAnswer == this.answer;
    }
  }
};
</script>

<style scoped>
.question__form {
  font-size: 32px;
}
input {
  font-size: 32px;
  border: none;
  border-bottom: 1px solid #333;
  outline: none;
  width: 100px;
}
</style>
