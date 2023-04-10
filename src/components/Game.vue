<template>
  <div class="game container">
    <div v-if="!end">
      <Question
        :questions="questions"
        :qIndex="qIndex"
        :color="color"
        :isDone="isDone"
        :correctAns="correctAns"
        :levels="levels"
        :lIndex="lIndex"
        @goTo="goTo"
        @checkCorrect="checkCorrect"
        @checkResult="checkResult"
        @handleNext="handleNext"
        @handleToast="handleToast"
      />
    </div>

    <div v-if="!end" class="levels">
      <Levels :levels="levels" :lIndex="lIndex" />
    </div>

    <div v-if="end" class="container">
      <End :score="score" :name="name" />
    </div>
  </div>
</template>

<script>
import Question from "./Question.vue";
import Levels from "./Levels.vue";
import End from "./End.vue";

export default {
  components: {
    Question,
    Levels,
    End,
  },
  props: ["name"],
  data() {
    return {
      questions: [
        {
          title: "What is the default value of the position property?",
          answers: [
            {
              text: "1. relative",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "2. static",
              correct: true,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "3. fixed",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "4. absolute",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
          ],
        },
        {
          title: "Which of these elements are all <table> elements?",
          answers: [
            {
              text: "1. <table><tr><td>",
              correct: true,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "2. <table><head><tfoot>",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "3. <thead><body><tr>",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "4. <table><tr><tt>",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
          ],
        },
        {
          title: "How can you open a link in a new tab/browser window?",
          answers: [
            {
              text: "1. <a href='url' target='_blank'>",
              correct: true,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "2. <a href='url' new>",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "3. <a href='url' target='new'>",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
          ],
        },
        {
          title:
            "How do you find the number with the highest value of x and y?",
          answers: [
            {
              text: "1. ceil(x, y)",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "2. top(x, y)",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "3. Math.ceil(x, y)",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "4. Math.max(x, y) ",
              correct: true,
              red: "",
              green: "",
              selected: false,
            },
          ],
        },
        {
          title: "How do you create a function in JavaScript?",
          answers: [
            {
              text: "1. function = myFunction()",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "2. function:myFunction()",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "3. function myFunction()",
              correct: true,
              red: "",
              green: "",
              selected: false,
            },
          ],
        },
        {
          title: "How can you detect the client's browser name?",
          answers: [
            {
              text: "1. client.navName",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "2. navigator.appName",
              correct: true,
              red: "",
              green: "",
              selected: false,
            },
            {
              text: "3. browser.name",
              correct: false,
              red: "",
              green: "",
              selected: false,
            },
          ],
        },
      ],
      qIndex: 0,
      color: "",
      isDone: false,
      correctAns: "",
      levels: [5000, 10000, 50000, 100000, 500000, 1000000],
      lIndex: "",
      score: "",
      end: false,
    };
  },
  mounted() {
    this.lIndex = this.questions.length;
  },
  methods: {
    checkCorrect(questions) {
      if (this.isDone == true) {
        const green = questions.filter((q) => q.correct == true);
        return (this.correctAns = green);
      }
    },
    checkResult(answer) {
      answer.selected = true;
      this.isDone = true;
      if (answer.correct == false) {
        this.handleToast({ type: "error", message: "Wrong!" });
        this.color = "5px solid #dc3545";
        answer.red = true;
        answer.green = false;
        if (this.lIndex < this.levels.length) {
          this.lIndex = this.lIndex + 0;
        } else return this.lIndex;
        console.log("false ");
      } else {
        this.handleToast({ type: "success", message: "Correct!" });
        this.color = "5px solid #028202";
        answer.green = true;
        answer.red = false;
        this.lIndex = this.lIndex - 1;
        console.log("true");
      }
    },
    handleNext() {
      this.handleScore();
      //Dovrsiti!
      if (this.qIndex < this.questions.length - 1) {
        setTimeout(() => {
          this.qIndex = this.qIndex + 1;
          this.isDone = false;
        }, 3000);
        this.handleToast({
          type: "success",
          message: "Correct answer is " + this.correctAns[0].text,
        });
      } else {
        console.log("end");
        this.end = true;
      }
      console.log(this.score);
    },
    handleToast(values) {
      this.$toast.show(values.message, {
        type: values.type,
        position: "top",
        duration: 2000,
      });
    },
    handleScore() {
      return (this.score = this.levels[this.lIndex]);
    },
  },
};
</script>

<style lang="scss">
.game {
  flex-direction: row;
  justify-content: space-between;
  width: 100%;
  padding: 1rem;
  height: 400px;

  .levels {
    border: 3px solid goldenrod;
    border-radius: 10px;
    height: 100%;
    width: 200px;
    padding: 1rem;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    background: url("../assets/Dark Knight.jpg");

    div {
      flex: 1;
      border: 1.5px solid black;
      border-radius: 50%;
      overflow: hidden;
      background: url("../assets/Between Night and Day.jpg");
      background-size: cover;
      width: 100%;
      margin-bottom: 5px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-weight: bold;
    }
    .active {
      background: url("../assets/Dark Knight.jpg");
    }
  }
}
</style>
