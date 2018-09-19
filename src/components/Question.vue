<template>
  <form class="question__form" @submit.prevent="onSubmit">
    <label>
      {{ question.x }} {{ question.action }} {{ question.y }} =
      <input type="text" v-model.number="userAnswer" ref="userInput" autofocus>
    </label>
  </form>
</template>

<script>
function getRandomInt(min, max) {
  const diff = max - min;
  return Math.floor(Math.random() * diff) + min;
}

function getRandomChoice(choices) {
  let index = Math.floor(Math.random() * choices.length);
  return choices[index];
}

class Question {
  constructor() {
    this.x = getRandomInt(0, 100);
    this.y = getRandomInt(0, 100);
    this.action = getRandomChoice('+-');

    if (this.action === '+') {
      this.answer = this.x + this.y;
    } else {
      this.answer = this.x - this.y;
    }
  }

  check(answer) {
    return this.answer === answer;
  }
}

export default {
  name: "Question",
  data() {
    return {
      question: new Question(),
      userAnswer: null,
    }
  },

  mounted() {
    this.$refs.userInput.focus();
  },
  
  methods: {
    onSubmit() {
      console.log('submit');
      if (this.question.check(this.userAnswer)) {
        console.log('good');
        this.$emit('success');
        this.question = new Question();
      } else {
        console.log('not good');
        this.$emit('onError');
      }
      this.userAnswer = null;
    },
    
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
  /* border-bottom: 1px solid #eee; */
  outline: none;
  width: 100px;
  text-align: center;
}
</style>
