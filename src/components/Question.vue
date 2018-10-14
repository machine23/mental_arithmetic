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
  constructor(min=0, max=100) {
    this.x = getRandomInt(min, max);
    this.y = getRandomInt(min, max);
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
      question: new Question(this.min, this.max),
      userAnswer: null,
    }
  },
  props: {
    min: {
      type: Number,
      default: 0
    },
    max: {
      type: Number,
      default: 100
    },
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
        this.question = new Question(this.min, this.max);
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
  font-size: 52px;
  padding: 18px;
  margin-top: 60px;
  margin-bottom: 40px;
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
