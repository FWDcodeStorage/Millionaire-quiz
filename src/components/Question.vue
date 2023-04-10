<template>
  <Transition name="fade">
    <div class="question" :style="{ border: color }">
      <h2>{{ questions[qIndex].title }}</h2>
      <div class="answers">
        <div
          class="answer"
          v-for="answer in questions[qIndex].answers"
          :class="{ false: answer.red, true: answer.green, done: isDone }"
          @click="result(answer), correct(questions[qIndex].answers)"
        >
          <h4>{{ answer.text }}</h4>
        </div>
      </div>
      <div class="btns" v-if="isDone">
        <button class="next" @click.prevent="next">Next</button>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {
  props: ["questions", "qIndex", "color", "isDone", "correctAns"],
  data() {
    return {};
  },
  methods: {
    correct(questions) {
      this.$emit("checkCorrect", questions);
    },
    result(answer) {
      this.$emit("checkResult", answer);
    },
    next() {
      this.$emit("handleNext");
    },
  },
};
</script>

<style lang="scss">
.question {
  border: 3px solid goldenrod;
  border-radius: 15px;
  height: 100%;
  width: 600px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-family: Noto Serif, serif;

  h2 {
    font-size: 1.2rem;
    color: goldenrod;
    letter-spacing: 2px;
  }
}
.answers {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin: 1rem 1rem;
  //   padding: 5px auto;
  width: 90%;
  cursor: pointer;

  .answer {
    height: 40px;
    width: 100%;
    padding: 5px auto;
    border: 2px solid goldenrod;
    border-radius: 5px;
    color: goldenrod;
    font-size: 15px;
    margin: 0.1rem 0;
    display: flex;
    justify-content: center;
    align-items: center;

    &:hover {
      background: #2c4053;
    }
  }
}
.false {
  color: #4a4a4a;
  background: #dc3545;
}
.true {
  background: #028202;
  color: whitesmoke;
}
.done {
  pointer-events: none;
  cursor: not-allowed;
}
.c-toast-container {
  position: fixed;
  top: 5%;
  left: 5%;
}
.c-toast-container .c-toast {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.e-toast-container .e-toast .e-toast-message .e-toast-title {
  color: #2e5c7e;
  font-size: 1.5rem;
  font-weight: bold;
  font-family: Noto Serif, serif;
}
</style>
