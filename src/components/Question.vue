<template>
  <form class="question__form" @submit.prevent="onSubmit">
    <label>
      {{ question.toString() }} =
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
  constructor(min=0, max=100, numItems=2) {
    if (numItems < 2) numItems = 2;
    this.items = Array.from({ length: numItems }, () => getRandomInt(min, max));
    this.actions = Array.from({ length: numItems - 1 }, () => getRandomChoice('+-'));

    this.answer = this.items[0];
    for (let i = 1; i < numItems; i++) {
      let action = this.actions[i-1];
      if (action === '+') {
        this.answer += this.items[i];
      } else {
        this.answer -= this.items[i];
      }
    }
  }

  check(answer) {
    return this.answer === answer;
  }

  toString() {
    let ret = this.items[0].toString() + ' ';
    for (let i = 1; i < this.items.length; i++) {
      ret += this.actions[i-1] + ' ' + this.items[i] + ' ';
    }
    return ret;
  }
}

export default {
  name: "Question",
  data() {
    return {
      question: new Question(this.min, this.max, this.numItems),
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
    numItems: {
      type: Number,
      // default: 2,
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
        this.question = new Question(this.min, this.max, this.numItems);
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
  margin-bottom: 60px;
}
input {
  font-size: 52px;
  border: none;
  /* border-bottom: 1px solid #eee; */
  outline: none;
  width: 100px;
  text-align: center;
}
</style>
